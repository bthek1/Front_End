# Responsive and Multiplatform

One design across widths, input methods, platforms and languages.

Author

Benedict Thekkel

Responsive design started as a layout problem and is now four problems that happen to arrive together:

1.  **Viewport**: a layout that works from a 320 px phone to a 2560 px monitor.
2.  **Input**: the same interface driven by finger, mouse, keyboard, stylus or voice.
3.  **Platform**: the conventions of iOS, Android, web and desktop, which genuinely differ.
4.  **Language**: text that expands 30 percent in German and runs right to left in Arabic.

Treating only the first one is what produces an interface that reflows beautifully and then cannot be operated with a thumb, or that looks correct in English and breaks in Finnish.

The governing idea for all four is the same: **describe intent and constraints rather than fixed outcomes.** A layout that says “these cards should each be at least 16 rem wide and fill the row” adapts by itself. A layout that says “three columns at 1024 px” needs a new rule for every situation you did not anticipate.

------------------------------------------------------------------------

## 1. Mobile first, and what it actually means

Mobile first is not about phones. It is about designing under the tightest constraint so the result is a prioritised interface rather than a compressed one.

![](data:image/svg+xml;base64,PHN2ZyB2aWV3Ym94PSIwIDAgNjQwIDIxMCIgd2lkdGg9IjEwMCUiIHN0eWxlPSJtYXgtd2lkdGg6NjQwcHgiIHJvbGU9ImltZyIgYXJpYS1sYWJlbD0iVGhlIHNhbWUgcGFnZSBhdCB0aHJlZSB3aWR0aHM6IHNpbmdsZSBjb2x1bW4gb24gbW9iaWxlLCB0d28gY29sdW1ucyBvbiB0YWJsZXQsIHRocmVlIGNvbHVtbnMgd2l0aCBhIHNpZGViYXIgb24gZGVza3RvcCI+Cjwvc3ZnPg==)

360 px768 px1280 px

stacked2 up3 up + aside

**What the constraint forces.** On a 360 px screen you cannot fit six equally important things, so you have to decide which one matters. That decision is the useful output, and it improves the desktop design too. Going the other direction, the desktop design has room for everything, so nothing gets prioritised and the mobile version becomes an exercise in hiding.

**Progressive enhancement is the same idea in code.** Write the single-column stacked case as the base, then add complexity at wider widths with `min-width` queries. The base case then works when a query fails, when CSS is partially loaded, and in a reader mode.

**It is not an excuse to remove functionality.** Hiding features on small screens assumes phones are used for lighter tasks, which was never reliably true and is now clearly false. Reorganise, do not amputate. If something genuinely cannot fit, it needs a different presentation rather than a `display: none`.

------------------------------------------------------------------------

## 2. Breakpoints come from content, not devices

Chasing device sizes is a losing game, because the list changes yearly and users resize windows anyway.

**Find breakpoints by resizing until the layout looks wrong.** That width is a breakpoint. It will not be a round number and it does not need to be. A layout whose cards get too narrow at 690 px gets a rule at 690 px.

A conventional starting set, understood as content thresholds rather than devices:

``` css
/* Base: narrowest case, no query at all */
.grid { display: grid; gap: 1rem; grid-template-columns: 1fr; }

@media (min-width: 40rem)  { .grid { grid-template-columns: repeat(2, 1fr); } }  /* ~640px */
@media (min-width: 64rem)  { .grid { grid-template-columns: repeat(3, 1fr); } }  /* ~1024px */
@media (min-width: 90rem)  { .page { grid-template-columns: 16rem 1fr; } }       /* sidebar appears */
```

**Use `rem` in media queries, not `px`.** A `rem`-based query respects a user who has increased their default font size, so the layout reflows at the width where their text actually needs more room. A `px` query ignores them.

**Prefer techniques that need no breakpoint at all.** Every breakpoint is a maintenance cost and a place for bugs, so the best layout rule is one that adapts continuously:

``` css
/* Cards wrap by themselves: no queries, no magic numbers */
.cards { display: grid; gap: 1rem; grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr)); }

/* Flex items that wrap when they cannot hold their basis */
.toolbar { display: flex; flex-wrap: wrap; gap: .5rem; }

/* A sidebar that becomes a stack with no query: the Every Layout "switcher" */
.with-aside { display: flex; flex-wrap: wrap; gap: 1.5rem; }
.with-aside > .main  { flex: 1 1 30rem; }   /* wraps when under 30rem */
.with-aside > .aside { flex: 1 1 14rem; }
```

------------------------------------------------------------------------

## 3. Fluid type and space

Stepping font size at breakpoints leaves awkward widths where the type is wrong. `clamp()` interpolates continuously instead.

``` css
:root {
  /* clamp(minimum, preferred, maximum) */
  --text-body: clamp(1rem, 0.95rem + 0.25vw, 1.125rem);
  --text-h1:   clamp(1.75rem, 1.4rem + 2.2vw, 3rem);
  --space-section: clamp(2rem, 1rem + 4vw, 5rem);
}
h1 { font-size: var(--text-h1); line-height: 1.15; }
```

**Always include a `rem` term in the preferred value**, as above. A pure `vw` value such as `clamp(1rem, 4vw, 2rem)` breaks zoom: `vw` does not respond to the user’s zoom or font-size setting, so the text can refuse to grow, which is a WCAG failure. Mixing a `rem` term back in keeps it responsive to both.

**Keep the measure capped independently.** Fluid type without a width cap gives you a 30-word line on a wide monitor. Cap the container at a readable measure (`max-width: 66ch`) and let type scale within it.

**Container queries, for components that do not know where they live.** A card in a sidebar and the same card in a full-width region want different internal layouts, and a viewport query cannot tell them apart. This is the actual fix for the oldest complaint about media queries:

``` css
.card-region { container-type: inline-size; container-name: card; }

@container card (min-width: 30rem) {
  .card { display: grid; grid-template-columns: 8rem 1fr; gap: 1rem; }
}
```

Container queries are supported across current browsers and are usually the right tool for component-level responsiveness. Media queries remain correct for page-level layout and for things that genuinely depend on the device, such as `prefers-reduced-motion`.

------------------------------------------------------------------------

## 4. Input: touch, pointer, keyboard

Width tells you nothing about how the device is being driven. A 1920 px touchscreen kiosk and a 1920 px desktop need different target sizes, and a tablet with a keyboard is both.

**Design for the coarsest input you expect, then enhance.** Touch-sized targets are perfectly usable with a mouse; mouse-sized targets are not usable with a thumb.

| Guidance | Minimum target |
|----|----|
| WCAG 2.2 (2.5.8, AA) | 24 by 24 CSS px, with spacing exceptions |
| Apple HIG | 44 by 44 pt |
| Material Design | 48 by 48 dp |
| Practical working rule | 44 to 48 px, with 8 px clearance between adjacent targets |

``` css
/* Feature queries for input, not guesses from width */
@media (pointer: coarse) {
  .btn { min-height: 2.75rem; min-width: 2.75rem; }   /* 44px */
}
@media (hover: hover) and (pointer: fine) {
  .row:hover .actions { opacity: 1; }                  /* reveal on hover is mouse-only */
}
```

**Never make hover the only path to anything.** `hover: hover` is the query that tells you hover exists, and the reveal-on-hover pattern needs an always-visible or focus-triggered equivalent for touch and keyboard users. A row of actions that appears only on mouse hover is invisible on every phone.

**Keyboard is not optional and is not only for accessibility.** Power users on desktop navigate by keyboard because it is faster. That means a visible focus ring, a logical tab order, Escape closing overlays, Enter submitting, and arrow keys working within composite widgets such as menus and tab lists. Full treatment in [Accessibility](../UI_UX/accessibility.llms.md).

**Thumb reach matters on phones.** The bottom half of a large phone screen is comfortable one-handed; the top corners are not. Primary actions belong low, which is why mobile operating systems moved navigation to the bottom. Destructive actions should not sit where a thumb rests.

**Do not assume touch means small, or mouse means large.** Test the combinations you actually ship to.

------------------------------------------------------------------------

## 5. Platform conventions

Cross-platform does not mean identical. Users learn their platform, and Jakob’s law says they will expect your app to behave like the others on it.

| Concern | iOS | Android | Web |
|----|----|----|----|
| Back navigation | Swipe from left edge, back button top left | System back gesture or button, always available | Browser back must work, including after a modal |
| Primary navigation | Bottom tab bar, up to 5 | Bottom navigation or navigation drawer | Top navigation is still the norm |
| Action placement | Top-right for confirm; bottom sheets common | Floating action button for the primary action | Bottom-right in dialogs, top-right in toolbars |
| Dialog buttons | Cancel left, confirm right | Dismiss left, confirm right, text buttons | Follow the platform your users came from |
| Scroll behaviour | Rubber-band overscroll | Overscroll glow or stretch | Do not reimplement either |
| Typography | SF Pro | Roboto | System stack |
| Settings | Often in the OS Settings app | In-app | In-app |

**What must be honoured versus what can be shared.** Navigation model, back behaviour, share and permission flows, and text selection are platform property. Layout, content, colour, iconography style and tone of voice can be shared. Getting this the wrong way round produces an app that feels foreign on both platforms.

**On the web, specific platform obligations that are easy to miss:**

- **The back button must work.** Opening a modal should be a history entry, or back exits your app entirely from the user’s point of view. This is the most common web app violation.
- **Deep links must work.** Every meaningful state needs an addressable URL, including filters and tabs.
- **Refresh must not lose state.** Someone will press it.
- **Do not hijack scroll, zoom, text selection, or the context menu.** Each removes a capability the user already had.

**Flutter makes this an explicit decision** by offering both Material and Cupertino widget sets. See [Widgets](../Flutter/widgets.llms.md) for how that works in practice.

------------------------------------------------------------------------

## 6. Density and data-heavy interfaces

Comfortable spacing is the right default and the wrong answer for someone who stares at a table of 400 rows all day. Density is a legitimate mode, not a failure of restraint.

**Offer a density setting when a view is genuinely data-heavy**, and drive it from tokens rather than a second stylesheet:

``` css
[data-density="comfortable"] { --row-h: 3rem;   --cell-pad: .75rem; --text-table: 0.9375rem; }
[data-density="compact"]     { --row-h: 2.25rem; --cell-pad: .375rem; --text-table: 0.8125rem; }
```

**Tables are the hard case on small screens.** Four approaches, each right in different circumstances:

| Approach | When it works |
|----|----|
| Horizontal scroll in a container, with the first column sticky | Many columns of genuinely comparable data |
| Collapse each row into a card | Few columns, each row read individually |
| Show 2 or 3 priority columns, expand a row for the rest | A clear priority order exists |
| Replace with a list plus a detail view | The row is really an object with its own page |

The one thing not to do is shrink the text until it fits. Also: a horizontally scrolling table needs its own `overflow-x: auto` container so the page itself never scrolls sideways, and it needs to be keyboard scrollable, which means it must be focusable.

**Do not confuse dense with cramped.** Density reduces padding and font size on a consistent scale. Cramped is what happens when spacing is reduced unevenly and grouping is lost.

------------------------------------------------------------------------

## 7. Internationalisation and right-to-left

Even a product shipping only in English benefits from these habits, because they are the same habits that survive a long label.

**Text expands.** German and Finnish routinely run 30 percent longer than English, and short UI strings can double. Russian and Greek expand too. A button sized exactly to “Save” breaks on “Speichern”.

- Never size a control to its English label. Let it grow, and test with the longest string you have.
- Avoid text in images, which cannot be translated.
- Do not concatenate sentences from fragments. Word order differs between languages, so pass a whole parameterised string to the translator.
- Allow two lines where a label might wrap, rather than clipping with an ellipsis.

**Use logical CSS properties**, which then handle right-to-left for free:

``` css
/* Physical: breaks in Arabic and Hebrew */
.card { margin-left: 1rem; padding-right: .5rem; text-align: left; border-left: 2px solid; }

/* Logical: flips automatically with the document direction */
.card { margin-inline-start: 1rem; padding-inline-end: .5rem; text-align: start; border-inline-start: 2px solid; }
```

**What flips in RTL and what does not.** Layout, reading order, alignment, and progress direction flip. Directional icons such as back arrows, undo and indentation flip. What does **not** flip: clocks, media playback controls, musical notation, and most logos. Numbers stay left to right even within RTL text.

**Formatting belongs to the locale, not to your code.** Dates, numbers, currencies, name order, address shape, first day of the week, and pluralisation rules all vary, and several languages have more than two plural forms. Use the platform’s internationalisation API:

``` js
new Intl.DateTimeFormat('de-DE', { dateStyle: 'long' }).format(new Date());
new Intl.NumberFormat('en-AU', { style: 'currency', currency: 'AUD' }).format(1234.5);
new Intl.RelativeTimeFormat('en').format(-3, 'day');
```

**Also.** Do not assume a name splits into first and last, do not require a postcode format, do not validate phone numbers against one country’s pattern, and store timestamps in UTC while displaying in the user’s timezone.

------------------------------------------------------------------------

## 8. Assets, performance and perceived speed

Responsive design includes not sending a 3 MB image to a phone on mobile data. Performance is part of the experience, not a separate engineering concern, because a slow interface is an unusable one.

``` html
<!-- Right size for the layout slot, right format for the browser -->
<img src="chart-800.webp"
     srcset="chart-400.webp 400w, chart-800.webp 800w, chart-1600.webp 1600w"
     sizes="(min-width: 64rem) 50vw, 100vw"
     width="800" height="450" loading="lazy" decoding="async"
     alt="Monthly usage, rising from 210 to 265 kWh between January and October">
```

**Always set `width` and `height`** (or `aspect-ratio`). Without them the page reflows when each image lands, which is layout shift, and it is one of the most irritating things an interface can do to someone who has started reading.

**The three Core Web Vitals, as design concerns:**

| Metric | Measures | Design lever |
|----|----|----|
| **LCP** | When the largest element renders | Do not make a hero image or a chart the first paint; keep fonts from blocking |
| **INP** | Responsiveness to interaction | Avoid work on the main thread during input; show immediate acknowledgement |
| **CLS** | Unexpected layout movement | Reserve space for images, ads, banners and async content |

**Reserve space for anything asynchronous.** A cookie banner, a promotion bar or a late-loading chart that pushes content down after the user started reading is a design failure with a metric attached.

**Fonts are usually the largest avoidable cost.** Subset them, use `font-display: swap` so text is readable immediately, and preload only the one face used above the fold. A system font stack costs nothing at all.

**Respect metered and slow connections.** `prefers-reduced-data` exists, images are the bulk of most pages, and autoplaying video on a phone is a real cost to someone on a limited plan.

[Website Metrics](../0_website_metrics.llms.md) covers measurement, and [Webpack](../webpack.llms.md) covers the bundling side.

------------------------------------------------------------------------

## 9. Testing across the matrix

Checking three widths in a browser’s device toolbar is the beginning, not the test.

**The checks worth building into a routine:**

- **Resize continuously**, not by breakpoint. Bugs live between breakpoints, where a heading wraps to three lines or a toolbar overlaps.
- **320 px width.** Still the sensible floor, and it catches most overflow problems.
- **Browser zoom to 200 percent**, and text-only zoom to 200 percent. WCAG requires content to work at 200 percent, and this is where fixed heights and `vw`-only type fail.
- **A real phone, on real mobile data.** Emulators do not reproduce touch accuracy, thumb reach, sunlight, or latency.
- **Keyboard only.** Tab through the whole page with the mouse untouched.
- **A screen reader**, on at least one page per pattern.
- **The longest translated string** you can find, or a pseudo-localised build that inflates every string.
- **`dir="rtl"` on the html element.** Ten seconds, and it exposes every physical margin in the codebase.
- **`prefers-reduced-motion: reduce`** and both colour schemes.
- **No horizontal page scroll at any width.** Easy to assert automatically.

``` js
// A fast overflow check in the console: what is wider than the viewport?
[...document.querySelectorAll('*')]
  .filter(el => el.getBoundingClientRect().right > document.documentElement.clientWidth + 1)
  .forEach(el => console.log(el, el.getBoundingClientRect().right));
```

**Automate the cheap parts.** Viewport screenshots at a few widths in CI catch regressions that manual checking will miss once the product has more than a few pages.

------------------------------------------------------------------------

## 10. How responsive design fails

- **Breakpoints copied from a device list**, so the layout breaks at every width not on the list.
- **`vw`-only fluid type**, which ignores zoom and fails WCAG.
- **Hover as the only affordance**, invisible on touch.
- **Mouse-sized targets on a touch screen.** Two 20 px icons, 2 px apart, in a table row.
- **Features hidden on mobile** instead of reorganised, on the assumption that phone users want less.
- **A table shrunk with `font-size`** until it technically fits.
- **Fixed heights on anything containing text.** The first long translation or large font setting clips it.
- **Physical CSS properties everywhere**, so right-to-left support becomes a rewrite.
- **Layout shift from late content**, punishing anyone who started reading.
- **`100vh` for a full-height mobile layout**, which is wrong while the browser chrome is visible. Use `100dvh`.
- **Tested only in a desktop browser’s device emulator**, which hides every input, latency and legibility problem.

------------------------------------------------------------------------

## Where this goes next

- [Accessibility](../UI_UX/accessibility.llms.md) covers zoom, reflow, target size and keyboard operation as formal requirements rather than good practice.
- [Design Systems and Tokens](../UI_UX/design_systems_and_tokens.llms.md) is where density modes, fluid scales and per-platform values are stored.
- [Visual Design Foundations](../UI_UX/visual_design_foundations.llms.md) covers the grid and measure rules this notebook applies.
- [Usability Evaluation](../UI_UX/usability_evaluation.llms.md) covers testing on real devices with real people.

Implementation: [CSS](../css.llms.md) for grid, flexbox, container queries and logical properties, [Bootstrap](../bootstrap.llms.md) for a ready-made responsive grid, [Flutter Widgets](../Flutter/widgets.llms.md) for the Material and Cupertino split, and [Website Metrics](../0_website_metrics.llms.md) for Core Web Vitals in practice.

------------------------------------------------------------------------

Back to top
