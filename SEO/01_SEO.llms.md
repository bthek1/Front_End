# SEO

SEO splits into three layers. As a full-stack dev you own one of them completely, share one, and should refuse the third.

Author

Benedict Thekkel

## Overview

| Layer | Owner | What it is |
|----|----|----|
| **Crawlability & rendering** | You, entirely | Can a bot fetch, parse, and index the page at all |
| **On-page markup & performance** | Shared | Titles, schema, internal links, Core Web Vitals |
| **Content & links** | Not you | What the page says, who links to it |

Almost every catastrophic SEO failure lives in layer 1 and is a bug, not a strategy problem. That’s your job.

------------------------------------------------------------------------

## 1. Rendering — the decision that determines everything else

**The rule: whatever a bot must index has to be in the initial HTML response.** Not after hydration. Not after a `useEffect`. In the bytes.

Googlebot renders JS via a second-pass render queue, but it’s delayed by hours to days, budget-limited, and drops out on errors. AI crawlers (GPTBot, ClaudeBot, PerplexityBot) mostly **don’t execute JavaScript at all**. In 2026 that makes CSR content effectively invisible to half of search.

Test it in one command:

``` bash
curl -sA "Mozilla/5.0 (compatible; GPTBot/1.0)" https://example.com/pricing | grep -c "Enterprise plan"
```

Zero means your page doesn’t exist to that crawler.

**Decision table:**

| Content type | Rendering | Why |
|----|----|----|
| Marketing, blog, docs, pricing, landing pages | SSG or server-rendered templates | Static, must rank, changes rarely |
| Public catalogue with frequent changes | SSR or ISR | Must rank, can’t pre-build all of it |
| Authenticated app | CSR, `noindex` | Nothing to rank |

**For your Django + React + Vite stack, the right answer is almost always: don’t SSR the SPA. Split the domain by responsibility.**

    /            → Django template (marketing)
    /pricing     → Django template
    /blog/*      → Django template + a Post model
    /docs/*      → static build (Astro/MkDocs) served by nginx
    /app/*       → React SPA, robots-disallowed, requires auth
    /api/*       → DRF

You get perfect crawlability with zero SSR infrastructure, no hydration mismatches, no Node runtime beside your Python one, and the SPA never needs to think about SEO. Adding Next.js in front of a Django backend to render marketing pages is architecture you’ll regret paying for.

If marketing pages genuinely must live in React (shared design system, marketing team edits components), use **build-time prerendering** — Vike or `vite-plugin-prerender` emitting static HTML per route — before you reach for full SSR.

------------------------------------------------------------------------

## 2. Status codes are ranking signals

Devs get this wrong constantly.

| Situation | Correct | Common bug |
|----|----|----|
| Page moved permanently | `301` | `302`, which doesn’t consolidate link equity |
| Temporary move | `302` / `307` | `301`, which is near-impossible to undo |
| Page gone forever | `410` | `404` (works, just slower to deindex) |
| Page doesn’t exist | `404` | **`200` with “not found” content** — soft 404, poisons your index |
| Maintenance | `503` + `Retry-After` | `200` with a splash page, or a `301` to `/maintenance` |
| Rate-limited bot | `429` | Blocking silently, or `403` |

The SPA catch-all is the classic offender. If Django serves `index.html` for any unmatched path, every typo URL returns 200 and gets indexed:

``` python
# urls.py — DON'T do this bare
re_path(r'^.*$', TemplateView.as_view(template_name='index.html'))
```

Scope it to the app prefix and let everything else 404:

``` python
re_path(r'^app/.*$', TemplateView.as_view(template_name='index.html'))
```

**Never redirect a 404 to the homepage.** It’s a soft-404 factory. 404 or 410, with a helpful page.

------------------------------------------------------------------------

## 3. URL design

- Lowercase, hyphens, no trailing-slash ambiguity. Django’s `APPEND_SLASH` picks one — make sure your React router and canonical tags agree with it. `/pricing` and `/pricing/` both returning 200 is duplicate content.
- No parameters where a path works. `/blog/seo-guide` not `/blog?id=42`.
- **Slugs are permanent.** Once indexed, changing one costs you a redirect and some equity. Store the slug on the model, never derive it from a mutable title on the fly.
- Include the ID if slugs can collide, but canonicalise: `/posts/42-my-title` should 301 to itself if the slug drifts.

``` python
def get(self, request, pk, slug):
    post = get_object_or_404(Post, pk=pk)
    if slug != post.slug:
        return redirect(post.get_absolute_url(), permanent=True)
    ...
```

------------------------------------------------------------------------

## 4. robots.txt and crawl budget

Crawl budget only matters above ~10k URLs, but wasted crawl is easy to create:

    User-agent: *
    Disallow: /app/
    Disallow: /api/
    Disallow: /*?sort=
    Disallow: /*?page=
    Allow: /

    Sitemap: https://example.com/sitemap.xml

Two things people get wrong:

- **`Disallow` ≠ `noindex`.** A disallowed URL can still be indexed from external links, appearing as a bare URL with no snippet. To keep something out of the index, *allow* the crawl and serve `X-Robots-Tag: noindex` or a meta robots tag. Blocking in robots.txt prevents Google from ever seeing the noindex.
- **Never disallow your JS/CSS.** Googlebot needs them to render.

For non-HTML responses use the header:

``` python
response['X-Robots-Tag'] = 'noindex, nofollow'
```

**Faceted navigation** is the single biggest crawl-budget sink. Filter combinations produce combinatorial URLs. Handle it with `rel=canonical` to the unfiltered page, `noindex` on filter combinations, and `Disallow` on the parameter patterns — all three, they do different jobs.

------------------------------------------------------------------------

## 5. Sitemaps

`django.contrib.sitemaps` handles this properly:

``` python
# sitemaps.py
from django.contrib.sitemaps import Sitemap
from .models import Post

class PostSitemap(Sitemap):
    changefreq = 'weekly'
    priority = 0.8
    protocol = 'https'

    def items(self):
        return Post.objects.filter(published=True).only('slug', 'updated_at')

    def lastmod(self, obj):
        return obj.updated_at

    def location(self, obj):
        return f'/blog/{obj.slug}'
```

``` python
# urls.py
from django.contrib.sitemaps.views import sitemap, index

sitemaps = {'posts': PostSitemap(), 'static': StaticViewSitemap()}
urlpatterns += [
    path('sitemap.xml', index, {'sitemaps': sitemaps}),
    path('sitemap-<section>.xml', sitemap, {'sitemaps': sitemaps},
         name='django.contrib.sitemaps.views.sitemap'),
]
```

Rules: 50,000 URLs and 50 MB per file, split with an index above that. `lastmod` must be **accurate** — Google ignores sitemaps where every page claims to have changed today. Only include canonical, indexable, 200-returning URLs. A sitemap full of 404s and redirects is a trust signal in the wrong direction.

------------------------------------------------------------------------

## 6. Head tags

Every indexable page needs, server-rendered:

``` html
<title>Patient Outcome Tracking Software | Recovery Metrics</title>
<meta name="description" content="…155 chars, written as ad copy…">
<link rel="canonical" href="https://example.com/features/outcomes">
<meta property="og:title" content="…">
<meta property="og:description" content="…">
<meta property="og:image" content="https://example.com/og/outcomes.png">
<meta property="og:url" content="https://example.com/features/outcomes">
<meta name="twitter:card" content="summary_large_image">
```

Canonical must be **absolute**, self-referencing by default, and consistent with what’s in your sitemap and your internal links. Three different opinions about the canonical URL is a very common and very silent bug.

If you do end up rendering meta in React, note that **React 19 hoists `<title>`, `<meta>` and `<link>` natively** — no `react-helmet` needed:

``` tsx
export function PostPage({ post }: { post: Post }) {
  return (
    <>
      <title>{post.title} | Recovery Metrics</title>
      <meta name="description" content={post.excerpt} />
      <link rel="canonical" href={`https://example.com/blog/${post.slug}`} />
      <article>{/* … */}</article>
    </>
  );
}
```

This only helps if the page is server-rendered or prerendered. In a pure CSR app the crawler never sees it.

------------------------------------------------------------------------

## 7. Structured data

JSON-LD in a `<script>` tag. Never microdata, never RDFa.

``` python
# templatetags or a context processor
import json
from django.utils.safestring import mark_safe

def article_schema(post):
    data = {
        "@context": "https://schema.org",
        "@type": "Article",
        "headline": post.title,
        "datePublished": post.published_at.isoformat(),
        "dateModified": post.updated_at.isoformat(),
        "author": {
            "@type": "Person",
            "name": post.author.get_full_name(),
            "url": post.author.profile_url,
            "sameAs": [post.author.linkedin_url],
        },
        "publisher": {
            "@type": "Organization",
            "name": "Recovery Metrics",
            "logo": {"@type": "ImageObject", "url": "https://…/logo.png"},
        },
    }
    return mark_safe(json.dumps(data))
```

Sitewide: `Organization` + `WebSite` on the homepage, `BreadcrumbList` on anything nested. Per-type: `Article`, `FAQPage`, `SoftwareApplication`, `Product` with `offers`.

**The schema must describe what’s visibly on the page.** Marking up FAQs that aren’t rendered is a manual-action risk. Validate in Search Console’s Rich Results Test, not just schema.org’s validator — Google supports a subset.

------------------------------------------------------------------------

## 8. Core Web Vitals, as engineering tasks

Field data (CrUX, 28-day p75) is what counts, not your Lighthouse score.

**LCP \< 2.5s** — usually the hero image or a web font.

``` html
<link rel="preload" as="image" href="/hero.avif" fetchpriority="high">
<img src="/hero.avif" width="1200" height="630" fetchpriority="high" alt="…">
```

Never lazy-load the LCP element. Self-host fonts with `font-display: swap` and `<link rel="preload" as="font" crossorigin>`. Subset them.

**INP \< 200ms** — long tasks on the main thread. In React: memoise expensive lists, virtualise anything over ~100 rows, and wrap non-urgent state updates:

``` tsx
const [isPending, startTransition] = useTransition();
startTransition(() => setFilter(next));
```

Break up long synchronous work with `scheduler.yield()` or `await new Promise(r => setTimeout(r, 0))`.

**CLS \< 0.1** — always set `width`/`height` (or `aspect-ratio`) on images and iframes, reserve space for ads/banners/cookie bars, and never inject content above existing content after load.

Vite specifics: `build.rollupOptions.output.manualChunks` to split vendor code, `import()` for route-level splitting, `vite-plugin-compression` for brotli. Check `rollup-plugin-visualizer` output — an unnoticed moment.js or full lodash import is the usual culprit.

Measure real users:

``` ts
import { onLCP, onINP, onCLS } from 'web-vitals';
[onLCP, onINP, onCLS].forEach(fn => fn(m =>
  navigator.sendBeacon('/api/vitals', JSON.stringify(m))
));
```

------------------------------------------------------------------------

## 9. Pagination and infinite scroll

Infinite scroll is invisible to crawlers unless you back it with real paginated URLs.

``` html
<!-- /blog?page=2 must exist, return 200, and be linked -->
<a href="/blog?page=2" rel="next">Next</a>
```

`rel=next`/`rel=prev` are no longer used by Google for indexing but still help other crawlers. The load-bearing requirement is that each page is a distinct, crawlable, linked URL. Self-canonical each page — do **not** canonical page 2 to page 1, that deindexes your deep content.

------------------------------------------------------------------------

## 10. Migrations and redirects

The highest-risk SEO event you’ll ever run is a redesign or replatform. Process:

1.  Crawl the old site (Screaming Frog) → full URL inventory with status codes.
2.  Pull top pages by clicks and impressions from Search Console API.
3.  Build an explicit **1:1 redirect map**. Not regex catch-alls to the homepage.
4.  Test the map in staging with an automated script asserting `old → 301 → new (200)`.
5.  Deploy, then monitor Search Console coverage and log 404s daily for a month.

Keep the map in code, not nginx config sprawl:

``` python
# a simple redirect middleware, or use django.contrib.redirects
REDIRECTS = {'/old-features': '/features', ...}

class LegacyRedirectMiddleware:
    def __init__(self, get_response): self.get_response = get_response
    def __call__(self, request):
        target = REDIRECTS.get(request.path.rstrip('/'))
        if target:
            return redirect(target, permanent=True)
        return self.get_response(request)
```

Redirect chains cost you — resolve `A → C` directly, not `A → B → C`.

------------------------------------------------------------------------

## 11. Internationalisation

If you serve AU and US:

``` html
<link rel="alternate" hreflang="en-au" href="https://example.com/au/pricing">
<link rel="alternate" hreflang="en-us" href="https://example.com/us/pricing">
<link rel="alternate" hreflang="x-default" href="https://example.com/pricing">
```

Must be **bidirectional** — every variant lists every other variant including itself, or Google ignores the whole set. Never auto-redirect by IP; it traps crawlers in the wrong region. Offer a banner instead.

------------------------------------------------------------------------

## 12. Bugs developers actually ship

- `noindex` left on production after a staging deploy. **This is the number-one catastrophic SEO bug in existence.** Guard it:

  ``` python
  # settings.py
  SEO_NOINDEX = env.bool('SEO_NOINDEX', default=not IS_PRODUCTION)
  ```

  and assert on it in a smoke test.

- Staging environment indexed because it was public with no auth. Basic auth on every non-prod environment.

- `Vary: User-Agent` missing on any device-conditional response.

- Cache busting that changes URLs of content, not just assets.

- CDN/WAF blocking Googlebot or GPTBot as suspicious traffic. Check your Cloudflare bot rules.

- Session IDs or tracking params in internal links generating infinite URL space.

- Lazy-loading everything including above-the-fold images.

- `Link` headers or canonical tags rendered client-side only.

- Soft 404s from the SPA catch-all (see §2).

------------------------------------------------------------------------

## 13. Put it in CI

SEO regressions are silent for weeks. Assert them like any other contract:

``` python
# tests/test_seo.py
import pytest
from django.urls import reverse

PUBLIC_PAGES = ['/', '/pricing', '/features', '/blog']

@pytest.mark.parametrize('url', PUBLIC_PAGES)
def test_page_is_indexable(client, url):
    r = client.get(url)
    assert r.status_code == 200
    html = r.content.decode()
    assert 'noindex' not in html
    assert '<link rel="canonical"' in html
    assert html.count('<h1') == 1
    assert 50 < len(extract_title(html)) < 60

def test_unknown_path_404s(client):
    assert client.get('/definitely-not-a-page').status_code == 404

def test_sitemap_urls_all_resolve(client):
    for url in parse_sitemap(client.get('/sitemap.xml').content):
        assert client.get(url).status_code == 200
```

Add **Lighthouse CI** with budgets that fail the build:

``` json
{
  "ci": {
    "assert": {
      "assertions": {
        "categories:seo": ["error", {"minScore": 0.95}],
        "largest-contentful-paint": ["error", {"maxNumericValue": 2500}],
        "cumulative-layout-shift": ["error", {"maxNumericValue": 0.1}]
      }
    }
  }
}
```

And a periodic Screaming Frog or `scrapy` crawl against production checking for broken internal links, redirect chains, missing canonicals, and duplicate titles.

------------------------------------------------------------------------

## 14. Monitoring

- **Search Console API** into your own database — the UI only keeps 16 months and won’t join against your data. Pull `query`, `page`, `clicks`, `impressions`, `position` daily into Postgres; it’s a small Celery task and gives you a real dataset.
- **Server logs segmented by user agent.** The ground truth for crawl behaviour. What’s Googlebot actually fetching, how often, and what status is it getting? Watch for GPTBot/ClaudeBot too — if they’re fetching but seeing empty shells, you have a rendering problem.
- **404 alerting** — a spike after deploy means a broken redirect map.
- **CrUX/RUM vitals** by page template, not sitewide averages.

------------------------------------------------------------------------

## What to hand back to marketing

Draw the line clearly, or you’ll spend your life editing meta descriptions. Give them a CMS field for `title`, `meta_description`, `og_image`, `slug`, and `canonical_override`, with validation on length. Everything else — rendering, status codes, schema generation, sitemaps, performance — stays in code, under test, owned by you.

------------------------------------------------------------------------

Back to top
