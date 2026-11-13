# Content Design and Motion

The words are the interface, and animation is an explanation: two things usually left until last.

Author

Benedict Thekkel

Two subjects sit together here because they share a property: both are treated as finishing touches, and both are load-bearing.

**Words are the interface.** A user reads a label, a button, an error and a heading before they use anything. More usability problems are fixed by rewriting a sentence than by moving an element, and it is the cheaper edit. “Content design” rather than “copywriting” is the usual term, because the job is structural: deciding what to say, in what order, and what to leave out.

**Motion is an explanation.** An animation’s job is to answer “what just happened and where did that come from”. Motion that does not answer a question is decoration, and decoration has a cost measured in milliseconds of attention and, for some people, in nausea.

------------------------------------------------------------------------

## 1. Voice and tone

**Voice is constant, tone varies by situation.** Voice is the product’s personality: plain, precise, warm, formal. Tone is how that personality adapts to the moment, and the mistake almost every product makes is to keep the tone identical everywhere.

| Situation                | Tone                                      |
|--------------------------|-------------------------------------------|
| Onboarding               | Encouraging, brief, concrete              |
| Routine confirmation     | Neutral, near-invisible                   |
| Error the user caused    | Plain and instructive, never blaming      |
| Error the system caused  | Direct, apologetic once, with a next step |
| Destructive confirmation | Serious and specific. No jokes            |
| Empty state              | Helpful, pointing at the first action     |
| Outage or data loss      | Factual, specific, no euphemism, no cheer |

**The jokes in errors problem.** A playful 404 is fine. The same playfulness on a failed payment or a lost draft reads as indifference, because the user is not amused, they are stuck. The rule is simple: **the higher the user’s stress, the plainer the language.**

**Write a short list of rules and hold to them.** Sentence case or title case for headings. First person (“your sites”) or second (“my sites”), never both. Oxford comma or not. Contractions allowed or not. These are minor individually and produce an incoherent product when unresolved.

------------------------------------------------------------------------

## 2. Microcopy

The small strings: buttons, labels, hints, placeholders, tooltips, empty states. Disproportionately important because they sit exactly at the point of action.

**Buttons name the action, specifically.**

``` text
Bad     OK              (OK to what?)
Bad     Submit          (nobody submits anything in real life)
Bad     Yes / No        (in a dialog, requires re-reading the question)
Good    Save changes
Good    Delete site
Good    Send invitation
```

The test: a button’s label should make sense when read on its own, because that is how a screen reader user and a hurried reader both encounter it.

**Never label a confirmation with OK and Cancel.** “Discard unsaved changes?” with OK and Cancel is genuinely ambiguous, because “cancel” could plausibly mean cancel the changes. “Discard changes” and “Keep editing” cannot be misread.

**Labels use the user’s words**, sourced from research and support tickets. This is the same rule as [Information Architecture](../UI_UX/information_architecture.llms.md) section 4 and it applies at every scale.

**Placeholders are not labels.** A placeholder disappears on typing, fails contrast requirements, breaks autofill, and is invisible to a user checking their entry. Use it only for a format example, in addition to a real label.

**Hints go before the input, not after.** Password requirements shown only after a rejection are a cause of avoidable failure. Put them above the field where they can be read before typing.

**Cut words that do nothing.**

``` text
Before  Please note that in order to continue, you will need to verify your email address.
After   Verify your email address to continue.

Before  There was a problem with your request. Please try again later.
After   Could not save. Your changes are kept. Try again.
```

------------------------------------------------------------------------

## 3. Error messages

An error message has three jobs: say **what happened**, say **why** if it helps, and say **what to do next**. Most shipped errors do the first badly and skip the third.

| Ingredient          | Example                                           |
|---------------------|---------------------------------------------------|
| What happened       | “Could not import the file.”                      |
| Why, if useful      | “Row 14 has no date.”                             |
| What to do          | “Add a date in the Date column and upload again.” |
| Preserve their work | The upload stays queued, the mapping is retained  |

**Do not blame the user.** “You entered an invalid date” versus “Enter a date as DD/MM/YYYY”. The second is shorter and tells them what to do.

**Do not expose internals.** “Error 422: unprocessable entity” and a stack trace tell the user nothing. Log the detail, show the human message, and include a reference code if support will need it.

**Be specific about which thing failed.** “Some fields are invalid” forces a hunt. Name the field, mark it, and if several failed, give a summary at the top of the form with links to each.

``` text
Bad     Invalid credentials.
Better  We could not find an account with that email. Check the address, or create an account.

Bad     Network error.
Better  Cannot reach the server. Your changes are saved on this device and will sync when you reconnect.

Bad     Password does not meet requirements.
Better  Passwords need at least 12 characters. Yours has 8.
```

**Distinguish these three cases** in wording, because the right next action differs:

- **The user made a recoverable mistake.** Tell them the fix.
- **The system failed transiently.** Offer retry, and say their work is safe.
- **The thing is not possible.** Explain the constraint rather than implying a retry will help.

**Never lose their input.** A failed submit that clears the form converts a small error into a lost task.

------------------------------------------------------------------------

## 4. Empty states and onboarding copy

The empty state is often the first screen a new user sees, so it is onboarding whether it was designed as onboarding or not. Three distinct emptiness cases need different words:

| Case | What it must say |
|----|----|
| **Nothing created yet** | What this screen is for, why it is useful, and the action that fills it |
| **Filtered to nothing** | Which filter excluded everything, and an offer to clear it |
| **Cleared by the user** (inbox zero, all tasks done) | Confirm the accomplishment. Do not push another action |

``` text
Weak      No data.

Better    No sites yet
          Add a site to start collecting meter readings. You can import
          several at once from a CSV.
          [ Add a site ]  [ Import from CSV ]

Filtered  No sites match "status: offline" in the last 24 hours.
          [ Clear filters ]
```

The distinction between the first two matters more than it looks: a user who has filtered to nothing and sees a first-run empty state reasonably concludes their data has been deleted.

**Onboarding copy.** Prefer doing over explaining. A tour of five tooltips is dismissed and forgotten; a prefilled example the user can edit teaches the same thing by use. If you must explain, explain at the moment of need rather than all at once at the start.

------------------------------------------------------------------------

## 5. Readability

**Plain language is not dumbing down.** It is the difference between a document that gets read and one that gets skimmed and misunderstood. Expert readers prefer plain language too, because they are busy.

- **Short sentences.** One idea each. Aim for an average around 15 to 20 words.
- **Active voice with a named actor.** “We will email you” rather than “an email will be sent”.
- **Front-load the sentence.** Put the conclusion first, then the qualification. People stop reading early.
- **Define jargon or drop it.** Use the user’s term and mention yours in brackets if the internal term appears elsewhere in the interface.
- **Avoid nominalisation.** “Make a decision” is “decide”. “Provide confirmation” is “confirm”.
- **Numerals for numbers**, and be consistent about formats.

**Structure for scanning**, because nobody reads an interface linearly:

- Meaningful headings that say what the section contains.
- Short paragraphs, three or four lines at most.
- Lists for anything enumerable, and a table for anything with two dimensions.
- Bold for the load-bearing phrase in a paragraph, used sparingly enough to still mean something.

**Write for the anxious reader.** People read interfaces while distracted, in a hurry, and sometimes worried about money or a deadline. Reading comprehension drops sharply under stress, which is the practical argument for plain language at exactly the moments it feels least sophisticated.

------------------------------------------------------------------------

## 6. Motion: what it is for

Animation in an interface should do one of four jobs. If it does none of them, remove it.

| Purpose | Example |
|----|----|
| **Show causality** | A panel growing from the button that opened it, so the relationship is visible |
| **Maintain continuity** | A list item expanding into a detail view, so the object persists rather than being replaced |
| **Direct attention** | A newly arrived row settling into place, so the change is noticed |
| **Mask latency** | A skeleton or progress animation, so a wait feels shorter |

**The test for any animation: what question does it answer?** “Where did this come from”, “where did that go”, “what changed”, “is it still working”. An animation that answers none of them is costing the user time.

**Origin matters more than duration.** A dialog that fades in from nowhere requires the user to work out its relationship to what they clicked. The same dialog scaling up from the button’s position explains itself. This is why transform-based motion from a source point reads as comprehensible while a generic fade reads as arbitrary.

**Do not animate to demonstrate craft.** The most-praised interfaces are mostly still. Motion draws the eye involuntarily, so every unnecessary animation is an interruption.

------------------------------------------------------------------------

## 7. Duration, easing and implementation

**Durations.** The workable range for interface motion is narrow, roughly 150 to 400 ms. Under about 100 ms the motion is not perceived as motion; over about 500 ms it feels sluggish, and on a frequently repeated interaction it becomes infuriating.

| Movement                                       | Duration      |
|------------------------------------------------|---------------|
| Small state change: hover, toggle, focus ring  | 100 to 150 ms |
| Element entering or leaving: dropdown, tooltip | 150 to 250 ms |
| Larger transition: panel, drawer, dialog       | 250 to 350 ms |
| Full-page or route transition                  | 300 to 400 ms |

**Scale duration with distance and size.** A tooltip crossing 8 px and a drawer crossing 400 px should not share a duration, or one will feel slow and the other abrupt.

**Easing carries meaning.**

Each curve below plots progress (vertical) against time (horizontal), which is exactly what the four `cubic-bezier` control points describe.

![](data:image/svg+xml;base64,PHN2ZyB2aWV3Ym94PSIwIDAgNjQwIDE1MCIgd2lkdGg9IjEwMCUiIHN0eWxlPSJtYXgtd2lkdGg6NjQwcHgiIHJvbGU9ImltZyIgYXJpYS1sYWJlbD0iRm91ciBlYXNpbmcgY3VydmVzOiBsaW5lYXIgaXMgYSBzdHJhaWdodCBkaWFnb25hbCwgZWFzZS1vdXQgcmlzZXMgc3RlZXBseSB0aGVuIGZsYXR0ZW5zLCBlYXNlLWluIHN0YXJ0cyBmbGF0IHRoZW4gYWNjZWxlcmF0ZXMsIGVhc2UtaW4tb3V0IGlzIGFuIFMgY3VydmUiPgo8ZyBmaWxsPSJub25lIiBzdHJva2U9ImN1cnJlbnRDb2xvciIgc3Ryb2tlLW9wYWNpdHk9Ii4yIj4gPHJlY3QgeD0iMjAiIHk9IjIwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjEwMCIgLz4gPHJlY3QgeD0iMTgwIiB5PSIyMCIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIxMDAiIC8+IDxyZWN0IHg9IjM0MCIgeT0iMjAiIHdpZHRoPSIxMDAiIGhlaWdodD0iMTAwIiAvPiA8cmVjdCB4PSI1MDAiIHk9IjIwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjEwMCIgLz4gPC9nPiA8ZyBmaWxsPSJub25lIiBzdHJva2U9IiMyNTYzZWIiIHN0cm9rZS13aWR0aD0iMiI+IDxwYXRoIGQ9Ik0yMCAxMjAgQyA1MyA4NywgODcgNTMsIDEyMCAyMCIgLz4gPHBhdGggZD0iTTE4MCAxMjAgQyAyMDAgMTIwLCAxODAgMjAsIDI4MCAyMCIgLz4gPHBhdGggZD0iTTM0MCAxMjAgQyAzODAgMTIwLCA0NDAgMjAsIDQ0MCAyMCIgLz4gPHBhdGggZD0iTTUwMCAxMjAgQyA1NDAgMTIwLCA1MjAgMjAsIDYwMCAyMCIgLz4gPC9nPiA8ZyBmb250LXNpemU9IjEwIiBmaWxsPSJjdXJyZW50Q29sb3IiPiA8dGV4dCB4PSIyMCIgeT0iMTM2Ij5saW5lYXI8L3RleHQ+IDx0ZXh0IHg9IjE4MCIgeT0iMTM2Ij5lYXNlLW91dDwvdGV4dD4gPHRleHQgeD0iMzQwIiB5PSIxMzYiPmVhc2UtaW48L3RleHQ+IDx0ZXh0IHg9IjUwMCIgeT0iMTM2Ij5lYXNlLWluLW91dDwvdGV4dD4gPC9nPiA8ZyBmb250LXNpemU9IjgiIGZpbGw9ImN1cnJlbnRDb2xvciIgZmlsbC1vcGFjaXR5PSIuNiI+IDx0ZXh0IHg9IjIwIiB5PSIxNCI+cHJvZ3Jlc3M8L3RleHQ+IDx0ZXh0IHg9IjE4MCIgeT0iMTQiPmZhc3Qgc3RhcnQsIGdlbnRsZSBzZXR0bGU8L3RleHQ+IDx0ZXh0IHg9IjM0MCIgeT0iMTQiPnNsb3cgc3RhcnQ6IHJlYWRzIGFzIGxhZzwvdGV4dD4gPHRleHQgeD0iNTAwIiB5PSIxNCI+c3ltbWV0cmljPC90ZXh0PiA8L2c+Cjwvc3ZnPg==)

| Easing | Use | Why |
|----|----|----|
| `ease-out` | Things entering | Fast start, gentle settle. The default choice for most UI motion |
| `ease-in` | Things leaving | Accelerates away; nobody needs to watch an exit finish |
| `ease-in-out` | Things moving between two on-screen positions | Symmetric, natural for a repositioning |
| `linear` | Continuous indicators, spinners, progress | Anything that should not appear to speed up or slow down |
| Spring | Playful or physical direct manipulation | Use sparingly; can overshoot into imprecision |

**Never `ease-in` for an entrance.** It starts slow, which reads as lag.

``` css
:root {
  --dur-fast: 150ms;
  --dur-base: 250ms;
  --ease-out: cubic-bezier(.2, 0, 0, 1);
  --ease-in:  cubic-bezier(.4, 0, 1, 1);
}

.panel {
  transition: transform var(--dur-base) var(--ease-out),
              opacity   var(--dur-fast) var(--ease-out);
}

/* Animate compositor-friendly properties only */
.panel[hidden="false"] { transform: translateY(0);      opacity: 1; }
.panel[hidden="true"]  { transform: translateY(-.5rem); opacity: 0; }
```

**Animate `transform` and `opacity`.** These run on the compositor and stay smooth. Animating `width`, `height`, `top`, `left` or `margin` forces layout on every frame and produces the stutter that makes an interface feel cheap. Where a size change is genuinely needed, `scale` is usually an acceptable substitute, and the modern alternatives are `view-transition` APIs or animating `grid-template-rows` with care.

**Respect reduced motion**, as covered in [Accessibility](../UI_UX/accessibility.llms.md):

``` css
@media (prefers-reduced-motion: reduce) {
  .panel { transition-duration: .01ms; }   /* keep the state change, drop the movement */
}
```

The preferred substitution is a cross-fade rather than nothing at all, so that the change is still perceivable.

------------------------------------------------------------------------

## 8. Perceived performance

How fast something feels is partly independent of how fast it is, and both halves are design decisions.

**Acknowledge instantly, complete eventually.** The interaction should visibly respond within about 100 ms even if the work takes two seconds. A pressed state, a spinner inside the button, a row appearing greyed out: all convert “did that work?” into “it is working”.

**Optimistic updates** apply the change immediately and reconcile in the background. Correct when failure is rare and reversible, wrong for anything with money or legal consequence. If you use them, the rollback must be visible and explained, never silent.

**Skeletons over spinners when you know the shape.** A skeleton communicates what is coming and prevents layout shift. A spinner communicates only that something is happening.

**Prefetch on intent.** Loading a route’s data on hover or on `pointerdown` rather than on click removes most of the perceived delay, because the work starts a few hundred milliseconds early.

**Never regress to a blank screen.** Keep the previous content visible with a loading indicator over it rather than clearing to empty, which destroys the user’s context and makes the wait feel longer.

**Do not fake progress.** A bar that fills to 90 percent and stops is worse than no bar, because it breaks trust in every subsequent one.

**The Doherty threshold**, around 400 ms, is the point below which people stay in flow rather than waiting. Worth treating as the design target for anything done repeatedly.

------------------------------------------------------------------------

## 9. How content and motion fail

**Content.**

- **Jargon in the interface**, taken from the database schema or the org chart.
- **OK and Cancel** on a question that cannot be answered with either.
- **Errors that blame and do not instruct.**
- **Placeholder text used as the label.**
- **Jokes in high-stress moments.**
- **Requirements revealed only after rejection.**
- **Inconsistent terms for one concept**, which makes the reader wonder whether they are the same thing.
- **Copy written last, by whoever was available**, and then never reviewed as a whole. Reading every string in a flow in sequence, out of the interface, exposes this immediately.

**Motion.**

- **Animation with no question to answer.** Decoration that costs attention.
- **Too slow**, especially on something done fifty times a day.
- **Animating layout properties**, producing stutter.
- **A fade with no origin**, leaving the user to work out the relationship.
- **Motion that blocks input** until it finishes. Interruptible always beats polished.
- **Ignoring `prefers-reduced-motion`.**
- **Parallax and scroll-jacking**, which take away a control the user already had.
- **An entrance animation on every page load**, which is a delay the user pays for on every visit.

------------------------------------------------------------------------

## Where this goes next

- [Interaction Design](../UI_UX/interaction_design.llms.md) holds the states these words and transitions belong to.
- [Accessibility](../UI_UX/accessibility.llms.md) covers plain language, reduced motion, and the requirement that labels be programmatically associated rather than merely nearby.
- [Information Architecture](../UI_UX/information_architecture.llms.md) covers labelling at the navigation scale.
- [Design Systems and Tokens](../UI_UX/design_systems_and_tokens.llms.md) is where durations, easings and tone rules are recorded so they stay consistent.
- [Usability Evaluation](../UI_UX/usability_evaluation.llms.md) is how you find out which words are not working, and wording problems are among the most common findings in any test.

Implementation: [CSS](../css.llms.md) for transitions and animations, and [Markdown](../markdown.llms.md) for the documentation formats this kind of content usually lives in.

------------------------------------------------------------------------

Back to top
