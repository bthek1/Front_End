# Visual Design Foundations

Hierarchy, layout, spacing, type and colour: the raw material of every interface surface.

Author

Benedict Thekkel

Visual design in an interface is not decoration. It is the mechanism by which a reader knows what matters, what belongs together, and where to look next, before reading a single word. A screen with correct content and no hierarchy is genuinely harder to use than a plain one with hierarchy, because the reader has to construct the structure themselves every time they look at it.

Five variables do nearly all of the work:

| Variable     | Controls                                                 |
|--------------|----------------------------------------------------------|
| **Size**     | Importance. The strongest and bluntest signal available  |
| **Weight**   | Emphasis without changing the space a thing occupies     |
| **Colour**   | Category and state, never meaning on its own             |
| **Space**    | Grouping. The most underused variable in most interfaces |
| **Position** | Reading order and relative priority                      |

The sections below take these in the order you would actually apply them: hierarchy first, then the grid that positions things, then the spacing scale, then type, then colour.

------------------------------------------------------------------------

## 1. Visual hierarchy

Before anything else, decide the order in which a first-time viewer should notice things. There should be one clear first place for the eye to land per screen, and a deliberate second and third.

![](data:image/svg+xml;base64,PHN2ZyB2aWV3Ym94PSIwIDAgNjQwIDIwMCIgd2lkdGg9IjEwMCUiIHN0eWxlPSJtYXgtd2lkdGg6NjQwcHgiIHJvbGU9ImltZyIgYXJpYS1sYWJlbD0iVHdvIHBhbmVsczogdGhlIGxlZnQgaGFzIG5vIGhpZXJhcmNoeSB3aXRoIGFsbCB0ZXh0IHRoZSBzYW1lIHNpemUsIHRoZSByaWdodCBoYXMgYSBjbGVhciBoZWFkaW5nLCBzdXBwb3J0aW5nIHRleHQsIGFuZCBvbmUgcHJpbWFyeSBidXR0b24iPgo8ZyBmaWxsPSJub25lIiBzdHJva2U9ImN1cnJlbnRDb2xvciIgc3Ryb2tlLW9wYWNpdHk9Ii4zNSI+IDxyZWN0IHg9IjgiIHk9IjgiIHdpZHRoPSIyOTYiIGhlaWdodD0iMTg0IiByeD0iNiIgLz4gPHJlY3QgeD0iMzM2IiB5PSI4IiB3aWR0aD0iMjk2IiBoZWlnaHQ9IjE4NCIgcng9IjYiIC8+IDwvZz4gPHRleHQgeD0iMjAiIHk9IjI4IiBmb250LXNpemU9IjEwIiBmaWxsPSJjdXJyZW50Q29sb3IiIGZpbGwtb3BhY2l0eT0iLjYiPk5PIEhJRVJBUkNIWTwvdGV4dD4gPHRleHQgeD0iMzQ4IiB5PSIyOCIgZm9udC1zaXplPSIxMCIgZmlsbD0iY3VycmVudENvbG9yIiBmaWxsLW9wYWNpdHk9Ii42Ij5ISUVSQVJDSFk8L3RleHQ+IDxnIGZpbGw9ImN1cnJlbnRDb2xvciIgZm9udC1zaXplPSIxMyI+IDx0ZXh0IHg9IjIwIiB5PSI2MCI+TW9udGhseSB1c2FnZSByZXBvcnQ8L3RleHQ+IDx0ZXh0IHg9IjIwIiB5PSI4MiI+WW91ciB1c2FnZSByb3NlIDEyJSB0aGlzIG1vbnRoPC90ZXh0PiA8dGV4dCB4PSIyMCIgeT0iMTA0Ij5Db21wYXJlZCB0byB0aGUgc2FtZSBtb250aCBsYXN0IHllYXI8L3RleHQ+IDx0ZXh0IHg9IjIwIiB5PSIxMjYiPlZpZXcgdGhlIGZ1bGwgYnJlYWtkb3duPC90ZXh0PiA8dGV4dCB4PSIyMCIgeT0iMTQ4Ij5Eb3dubG9hZCBDU1Y8L3RleHQ+IDx0ZXh0IHg9IjIwIiB5PSIxNzAiPk1hbmFnZSBhbGVydCB0aHJlc2hvbGRzPC90ZXh0PiA8L2c+IDx0ZXh0IHg9IjM0OCIgeT0iNjYiIGZvbnQtc2l6ZT0iMjAiIGZvbnQtd2VpZ2h0PSI3MDAiIGZpbGw9ImN1cnJlbnRDb2xvciI+VXNhZ2UgdXAgMTIlPC90ZXh0PiA8dGV4dCB4PSIzNDgiIHk9IjkwIiBmb250LXNpemU9IjEyIiBmaWxsPSJjdXJyZW50Q29sb3IiIGZpbGwtb3BhY2l0eT0iLjc1Ij5Nb250aGx5IHJlcG9ydCwgT2N0b2JlciAyMDI2PC90ZXh0PiA8dGV4dCB4PSIzNDgiIHk9IjExMiIgZm9udC1zaXplPSIxMSIgZmlsbD0iY3VycmVudENvbG9yIiBmaWxsLW9wYWNpdHk9Ii41NSI+Q29tcGFyZWQgd2l0aCBPY3RvYmVyIDIwMjU8L3RleHQ+IDxyZWN0IHg9IjM0OCIgeT0iMTI4IiB3aWR0aD0iMTEyIiBoZWlnaHQ9IjMwIiByeD0iNSIgZmlsbD0iIzI1NjNlYiIgLz4gPHRleHQgeD0iNDA0IiB5PSIxNDciIGZvbnQtc2l6ZT0iMTIiIGZpbGw9IiNmZmYiIHRleHQtYW5jaG9yPSJtaWRkbGUiPlZpZXcgYnJlYWtkb3duPC90ZXh0PiA8dGV4dCB4PSI0NzYiIHk9IjE0NyIgZm9udC1zaXplPSIxMiIgZmlsbD0iIzI1NjNlYiI+RG93bmxvYWQgQ1NWPC90ZXh0PiA8dGV4dCB4PSIzNDgiIHk9IjE4MCIgZm9udC1zaXplPSIxMSIgZmlsbD0iY3VycmVudENvbG9yIiBmaWxsLW9wYWNpdHk9Ii41NSI+TWFuYWdlIGFsZXJ0IHRocmVzaG9sZHM8L3RleHQ+Cjwvc3ZnPg==)

Both panels contain the same six pieces of information. The right one has decided which matters.

**The technique is contrast, and contrast requires difference.** Two headings at 17 px and 19 px do not read as two levels, they read as an inconsistency. If two things have different importance, make the difference obvious; if they have the same importance, make them identical.

**Squint at it.** Blur the screen, or look at it from across the room. Whatever still stands out is your real hierarchy, and it is frequently not the one you intended. This is the cheapest visual design test available.

**One primary action per view.** Three buttons of equal weight is the same as no primary action. Primary gets the filled treatment, secondary gets an outline or a plain text button, tertiary goes in a menu.

------------------------------------------------------------------------

## 2. Layout and grids

A grid exists so that alignment decisions are made once instead of per element. The 12-column grid is the common default because 12 divides by 2, 3, 4 and 6, giving halves, thirds, quarters and sixths without fractional widths.

![](data:image/svg+xml;base64,PHN2ZyB2aWV3Ym94PSIwIDAgNjQwIDE1MCIgd2lkdGg9IjEwMCUiIHN0eWxlPSJtYXgtd2lkdGg6NjQwcHgiIHJvbGU9ImltZyIgYXJpYS1sYWJlbD0iQSAxMiBjb2x1bW4gZ3JpZCB3aXRoIGd1dHRlcnMsIHNob3dpbmcgYSAxMi13aWRlIGhlYWRlciwgdGhlbiBhbiA4IHBsdXMgNCBzcGxpdCwgdGhlbiB0aHJlZSA0LXdpZGUgY2FyZHMiPgo8Zz4gPGcgZmlsbD0iY3VycmVudENvbG9yIiBmaWxsLW9wYWNpdHk9Ii4wOCI+IDxyZWN0IHg9IjE2IiB5PSIyNCIgd2lkdGg9IjQwIiBoZWlnaHQ9IjExMCIgLz48cmVjdCB4PSI2NCIgeT0iMjQiIHdpZHRoPSI0MCIgaGVpZ2h0PSIxMTAiIC8+IDxyZWN0IHg9IjExMiIgeT0iMjQiIHdpZHRoPSI0MCIgaGVpZ2h0PSIxMTAiIC8+PHJlY3QgeD0iMTYwIiB5PSIyNCIgd2lkdGg9IjQwIiBoZWlnaHQ9IjExMCIgLz4gPHJlY3QgeD0iMjA4IiB5PSIyNCIgd2lkdGg9IjQwIiBoZWlnaHQ9IjExMCIgLz48cmVjdCB4PSIyNTYiIHk9IjI0IiB3aWR0aD0iNDAiIGhlaWdodD0iMTEwIiAvPiA8cmVjdCB4PSIzMDQiIHk9IjI0IiB3aWR0aD0iNDAiIGhlaWdodD0iMTEwIiAvPjxyZWN0IHg9IjM1MiIgeT0iMjQiIHdpZHRoPSI0MCIgaGVpZ2h0PSIxMTAiIC8+IDxyZWN0IHg9IjQwMCIgeT0iMjQiIHdpZHRoPSI0MCIgaGVpZ2h0PSIxMTAiIC8+PHJlY3QgeD0iNDQ4IiB5PSIyNCIgd2lkdGg9IjQwIiBoZWlnaHQ9IjExMCIgLz4gPHJlY3QgeD0iNDk2IiB5PSIyNCIgd2lkdGg9IjQwIiBoZWlnaHQ9IjExMCIgLz48cmVjdCB4PSI1NDQiIHk9IjI0IiB3aWR0aD0iNDAiIGhlaWdodD0iMTEwIiAvPiA8L2c+IDx0ZXh0IHg9IjE2IiB5PSIxNiIgZm9udC1zaXplPSI5IiBmaWxsPSJjdXJyZW50Q29sb3IiIGZpbGwtb3BhY2l0eT0iLjYiPjEyIGNvbHVtbnMsIDggcHggZ3V0dGVycywgZml4ZWQgbWFyZ2luczwvdGV4dD4gPHJlY3QgeD0iMTYiIHk9IjI4IiB3aWR0aD0iNTY4IiBoZWlnaHQ9IjIyIiByeD0iMyIgZmlsbD0iIzI1NjNlYiIgZmlsbC1vcGFjaXR5PSIuNTUiIC8+IDx0ZXh0IHg9IjI0IiB5PSI0MyIgZm9udC1zaXplPSIxMCIgZmlsbD0iY3VycmVudENvbG9yIj5zcGFuIDEyPC90ZXh0PiA8cmVjdCB4PSIxNiIgeT0iNTgiIHdpZHRoPSIzNzYiIGhlaWdodD0iMzQiIHJ4PSIzIiBmaWxsPSIjMjU2M2ViIiBmaWxsLW9wYWNpdHk9Ii4zNSIgLz4gPHRleHQgeD0iMjQiIHk9Ijc5IiBmb250LXNpemU9IjEwIiBmaWxsPSJjdXJyZW50Q29sb3IiPnNwYW4gODwvdGV4dD4gPHJlY3QgeD0iNDAwIiB5PSI1OCIgd2lkdGg9IjE4NCIgaGVpZ2h0PSIzNCIgcng9IjMiIGZpbGw9IiMyNTYzZWIiIGZpbGwtb3BhY2l0eT0iLjIiIC8+IDx0ZXh0IHg9IjQwOCIgeT0iNzkiIGZvbnQtc2l6ZT0iMTAiIGZpbGw9ImN1cnJlbnRDb2xvciI+c3BhbiA0PC90ZXh0PiA8cmVjdCB4PSIxNiIgeT0iMTAwIiB3aWR0aD0iMTg0IiBoZWlnaHQ9IjMwIiByeD0iMyIgZmlsbD0iIzI1NjNlYiIgZmlsbC1vcGFjaXR5PSIuMjgiIC8+IDxyZWN0IHg9IjIwOCIgeT0iMTAwIiB3aWR0aD0iMTg0IiBoZWlnaHQ9IjMwIiByeD0iMyIgZmlsbD0iIzI1NjNlYiIgZmlsbC1vcGFjaXR5PSIuMjgiIC8+IDxyZWN0IHg9IjQwMCIgeT0iMTAwIiB3aWR0aD0iMTg0IiBoZWlnaHQ9IjMwIiByeD0iMyIgZmlsbD0iIzI1NjNlYiIgZmlsbC1vcGFjaXR5PSIuMjgiIC8+IDx0ZXh0IHg9IjI0IiB5PSIxMTkiIGZvbnQtc2l6ZT0iMTAiIGZpbGw9ImN1cnJlbnRDb2xvciI+NDwvdGV4dD4gPHRleHQgeD0iMjE2IiB5PSIxMTkiIGZvbnQtc2l6ZT0iMTAiIGZpbGw9ImN1cnJlbnRDb2xvciI+NDwvdGV4dD4gPHRleHQgeD0iNDA4IiB5PSIxMTkiIGZvbnQtc2l6ZT0iMTAiIGZpbGw9ImN1cnJlbnRDb2xvciI+NDwvdGV4dD4gPC9nPgo8L3N2Zz4=)

**In CSS you rarely need a column framework any more.** Grid and flexbox express the intent directly:

``` css
.page {
  display: grid;
  grid-template-columns: repeat(12, minmax(0, 1fr));
  gap: 1rem;
  max-width: 72rem;       /* a measure cap, not a device width */
  margin-inline: auto;
  padding-inline: 1rem;   /* the gutter that keeps text off the edge */
}
.main  { grid-column: span 8; }
.aside { grid-column: span 4; }

/* Auto-fitting cards need no breakpoints at all. */
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
  gap: 1rem;
}
```

Note `minmax(0, 1fr)` rather than `1fr`: without it, a long unbreakable string can force a column wider than its share and blow out the layout.

**Alignment is the cheapest quality signal there is.** Fewer alignment edges reads as more deliberate. Pick a left edge and hold it down the whole page; the eye notices a 3 px inconsistency without being able to name it.

**Cap the content width, not the viewport.** A text column should stop at a readable measure regardless of how wide the window is. See section 4.

------------------------------------------------------------------------

## 3. Spacing

Spacing is how grouping is communicated, and it is the variable most often left to chance. The mechanism is the Gestalt principle of proximity: things near each other are read as related, whatever the borders say.

![](data:image/svg+xml;base64,PHN2ZyB2aWV3Ym94PSIwIDAgNjQwIDEyOCIgd2lkdGg9IjEwMCUiIHN0eWxlPSJtYXgtd2lkdGg6NjQwcHgiIHJvbGU9ImltZyIgYXJpYS1sYWJlbD0iTGVmdDogYSBsYWJlbCBhbmQgZmllbGQgd2l0aCBldmVuIHNwYWNpbmcsIGFtYmlndW91cyBncm91cGluZy4gUmlnaHQ6IHRpZ2h0IGxhYmVsLXRvLWZpZWxkIHNwYWNpbmcgYW5kIHdpZGUgZ3JvdXAgc3BhY2luZywgc28gcGFpcnMgYXJlIG9idmlvdXMiPgo8ZyBmaWxsPSJub25lIiBzdHJva2U9ImN1cnJlbnRDb2xvciIgc3Ryb2tlLW9wYWNpdHk9Ii4zIj4gPHJlY3QgeD0iOCIgeT0iOCIgd2lkdGg9IjI5NiIgaGVpZ2h0PSIxMTIiIHJ4PSI2IiAvPjxyZWN0IHg9IjMzNiIgeT0iOCIgd2lkdGg9IjI5NiIgaGVpZ2h0PSIxMTIiIHJ4PSI2IiAvPiA8L2c+IDx0ZXh0IHg9IjIwIiB5PSIyNCIgZm9udC1zaXplPSI5IiBmaWxsPSJjdXJyZW50Q29sb3IiIGZpbGwtb3BhY2l0eT0iLjYiPkVWRU4gU1BBQ0lORzogcGFpcnMgdW5jbGVhcjwvdGV4dD4gPHRleHQgeD0iMzQ4IiB5PSIyNCIgZm9udC1zaXplPSI5IiBmaWxsPSJjdXJyZW50Q29sb3IiIGZpbGwtb3BhY2l0eT0iLjYiPlBST1hJTUlUWTogcGFpcnMgb2J2aW91czwvdGV4dD4gPGcgZm9udC1zaXplPSIxMCIgZmlsbD0iY3VycmVudENvbG9yIj4gPHRleHQgeD0iMjAiIHk9IjQ0Ij5TaXRlIG5hbWU8L3RleHQ+IDxyZWN0IHg9IjIwIiB5PSI1MCIgd2lkdGg9IjEzMCIgaGVpZ2h0PSIxNCIgcng9IjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iY3VycmVudENvbG9yIiBzdHJva2Utb3BhY2l0eT0iLjQ1IiAvPiA8dGV4dCB4PSIyMCIgeT0iODAiPk1ldGVyIElEPC90ZXh0PiA8cmVjdCB4PSIyMCIgeT0iODYiIHdpZHRoPSIxMzAiIGhlaWdodD0iMTQiIHJ4PSIyIiBmaWxsPSJub25lIiBzdHJva2U9ImN1cnJlbnRDb2xvciIgc3Ryb2tlLW9wYWNpdHk9Ii40NSIgLz4gPHRleHQgeD0iMzQ4IiB5PSI0MCI+U2l0ZSBuYW1lPC90ZXh0PiA8cmVjdCB4PSIzNDgiIHk9IjQ0IiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjE0IiByeD0iMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJjdXJyZW50Q29sb3IiIHN0cm9rZS1vcGFjaXR5PSIuNDUiIC8+IDx0ZXh0IHg9IjM0OCIgeT0iODgiPk1ldGVyIElEPC90ZXh0PiA8cmVjdCB4PSIzNDgiIHk9IjkyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjE0IiByeD0iMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJjdXJyZW50Q29sb3IiIHN0cm9rZS1vcGFjaXR5PSIuNDUiIC8+IDwvZz4gPGcgc3Ryb2tlPSIjMjU2M2ViIiBzdHJva2Utd2lkdGg9IjEiPiA8bGluZSB4MT0iMTcwIiB5MT0iNDQiIHgyPSIxNzAiIHkyPSI2NCI+PC9saW5lPjxsaW5lIHgxPSIxNjYiIHkxPSI0NCIgeDI9IjE3NCIgeTI9IjQ0Ij48L2xpbmU+PGxpbmUgeDE9IjE2NiIgeTE9IjY0IiB4Mj0iMTc0IiB5Mj0iNjQiPjwvbGluZT4gPGxpbmUgeDE9IjE3MCIgeTE9IjY0IiB4Mj0iMTcwIiB5Mj0iODYiPjwvbGluZT4gPGxpbmUgeDE9IjQ5OCIgeTE9IjMyIiB4Mj0iNDk4IiB5Mj0iNTgiPjwvbGluZT48bGluZSB4MT0iNDk0IiB5MT0iMzIiIHgyPSI1MDIiIHkyPSIzMiI+PC9saW5lPjxsaW5lIHgxPSI0OTQiIHkxPSI1OCIgeDI9IjUwMiIgeTI9IjU4Ij48L2xpbmU+IDxsaW5lIHgxPSI0OTgiIHkxPSI1OCIgeDI9IjQ5OCIgeTI9IjgwIj48L2xpbmU+PGxpbmUgeDE9IjQ5NCIgeTE9IjgwIiB4Mj0iNTAyIiB5Mj0iODAiPjwvbGluZT4gPC9nPiA8dGV4dCB4PSIxODAiIHk9IjU4IiBmb250LXNpemU9IjkiIGZpbGw9IiMyNTYzZWIiPjE2PC90ZXh0PiA8dGV4dCB4PSIxODAiIHk9IjgwIiBmb250LXNpemU9IjkiIGZpbGw9IiMyNTYzZWIiPjE2PC90ZXh0PiA8dGV4dCB4PSI1MDgiIHk9IjQ4IiBmb250LXNpemU9IjkiIGZpbGw9IiMyNTYzZWIiPjY8L3RleHQ+IDx0ZXh0IHg9IjUwOCIgeT0iNzQiIGZvbnQtc2l6ZT0iOSIgZmlsbD0iIzI1NjNlYiI+MjQ8L3RleHQ+Cjwvc3ZnPg==)

**The rule: space within a group must be smaller than space between groups.** A label 6 px from its field and 24 px from the next pair needs no lines, boxes or shading to be understood. If you find yourself adding borders to clarify grouping, the spacing is usually wrong.

**Use a scale, not arbitrary numbers.** A 4 px base with doubling steps is the common choice, since it lands on whole pixels at every zoom level and gives roughly the right granularity:

``` css
:root {
  --space-1: 0.25rem;  /*  4px  icon to label            */
  --space-2: 0.5rem;   /*  8px  inside a control          */
  --space-3: 0.75rem;  /* 12px  label to field            */
  --space-4: 1rem;     /* 16px  between fields            */
  --space-6: 1.5rem;   /* 24px  between field groups      */
  --space-8: 2rem;     /* 32px  between card sections     */
  --space-12: 3rem;    /* 48px  between page sections     */
  --space-16: 4rem;    /* 64px  major page divisions      */
}
```

Two habits that follow from a scale:

- **Only ever use values from it.** The moment a 13 px gap appears, the system stops guaranteeing rhythm, and the next person copies the 13.
- **Apply space in one direction.** Margin-bottom on stacked elements, or better, `gap` on the container. Mixing top and bottom margins makes collapsing margins your problem and every gap becomes a subtraction puzzle.

**White space is not wasted space.** The most common note on a first draft interface is that everything needs more room. Density is occasionally correct, for a trading screen or a log viewer, but it should be a decision you can defend rather than the result of filling the viewport.

------------------------------------------------------------------------

## 4. Typography

Most interface text is set by four decisions: the family, the scale, the measure, and the line height.

**A type scale gives you distinguishable sizes.** Pick a base of 16 px, because that is the browser default and shrinking it fights the user’s own settings, then generate steps by a ratio. 1.25 (major third) is a safe interface ratio; 1.2 is tighter for dense applications; 1.333 and above suits marketing pages.

![](data:image/svg+xml;base64,PHN2ZyB2aWV3Ym94PSIwIDAgNjQwIDE3NiIgd2lkdGg9IjEwMCUiIHN0eWxlPSJtYXgtd2lkdGg6NjQwcHgiIHJvbGU9ImltZyIgYXJpYS1sYWJlbD0iQSB0eXBlIHNjYWxlIGZyb20gMTIgdG8gMzkgcGl4ZWxzLCBlYWNoIHN0ZXAgbGFiZWxsZWQgd2l0aCBpdHMgc2l6ZSBhbmQgcm9sZSI+CjxnIGZpbGw9ImN1cnJlbnRDb2xvciI+IDx0ZXh0IHg9IjE2IiB5PSIyNiIgZm9udC1zaXplPSIxMiI+MTIgLyAxNiBjYXB0aW9uLCB0YWJsZSBtZXRhPC90ZXh0PiA8dGV4dCB4PSIxNiIgeT0iNTAiIGZvbnQtc2l6ZT0iMTQiPjE0IC8gMjAgc2Vjb25kYXJ5IGJvZHksIGxhYmVsczwvdGV4dD4gPHRleHQgeD0iMTYiIHk9Ijc2IiBmb250LXNpemU9IjE2Ij4xNiAvIDI0IGJvZHksIHRoZSBkZWZhdWx0PC90ZXh0PiA8dGV4dCB4PSIxNiIgeT0iMTA0IiBmb250LXNpemU9IjIwIiBmb250LXdlaWdodD0iNjAwIj4yMCAvIDI4IGgzPC90ZXh0PiA8dGV4dCB4PSIxNiIgeT0iMTM2IiBmb250LXNpemU9IjI1IiBmb250LXdlaWdodD0iNjAwIj4yNSAvIDMyIGgyPC90ZXh0PiA8dGV4dCB4PSIxNiIgeT0iMTcyIiBmb250LXNpemU9IjMxIiBmb250LXdlaWdodD0iNzAwIj4zMSAvIDQwIGgxPC90ZXh0PiA8L2c+Cjwvc3ZnPg==)

``` css
:root {
  --text-xs: 0.75rem;    /* 12px */
  --text-sm: 0.875rem;   /* 14px */
  --text-base: 1rem;     /* 16px */
  --text-lg: 1.25rem;    /* 20px */
  --text-xl: 1.5625rem;  /* 25px */
  --text-2xl: 1.9375rem; /* 31px */
}
```

**Measure: 45 to 75 characters per line, with 66 as a good target.** Beyond about 80 the eye loses the line when it returns to the left edge; below about 40 the rhythm breaks. Set it in `ch` units so it tracks the font rather than guessing pixel widths:

``` css
.prose { max-width: 66ch; }
```

**Line height scales inversely with size.** Body text wants 1.5; a large heading wants 1.1 to 1.25, because at that size generous leading pulls the words apart. Set line height unitless so it inherits proportionally.

**Weight and case.**

- Two or three weights are enough: regular for body, semibold or bold for headings, plus one more if you need it. Loading six weights costs real download time for a distinction nobody notices.
- **Avoid all caps for anything longer than a couple of words.** Uppercase removes the word shapes that fast reading depends on, which measurably slows reading.
- Light weights below 300 at small sizes fail contrast in practice even when the colour maths passes, because thin strokes carry less ink.

**Alignment.** Left-aligned (or start-aligned, which handles right-to-left correctly) for body text. Centre only short runs such as a heading or an empty-state message. Justified text creates rivers of white space in a browser, which lacks proper hyphenation control, so avoid it.

**Numbers in tables need tabular figures**, or the columns will not line up as the digits change:

``` css
.metric { font-variant-numeric: tabular-nums; }
```

**Use a system font stack unless a custom face earns its cost.** It renders instantly, matches the platform, and covers every script the user has installed.

``` css
body {
  font-family: system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
}
```

------------------------------------------------------------------------

## 5. Colour

The mistake with colour is treating it as a palette of pretty values. Treat it as a set of **roles** instead, each with a defined job, and pick values that satisfy those jobs.

| Role | Job |
|----|----|
| Surface / background | The ground everything sits on, usually two or three levels |
| Text | Primary, secondary, disabled: a small ramp, not one colour |
| Border | Separation where space alone is not enough |
| Accent / primary | One colour, for the primary action and active state |
| Semantic | Success, warning, danger, info. Fixed meanings, used nowhere else |

**Neutrals do most of the work.** A good interface is largely greys, with colour reserved for meaning. If everything is coloured, colour signals nothing. The 60-30-10 guideline is a reasonable starting ratio: 60 percent dominant neutral, 30 percent secondary, 10 percent accent.

**Build a ramp, not a swatch.** One hue at nine or ten lightness steps gives you hover states, borders, and tints without inventing new colours:

![](data:image/svg+xml;base64,PHN2ZyB2aWV3Ym94PSIwIDAgNjQwIDc0IiB3aWR0aD0iMTAwJSIgc3R5bGU9Im1heC13aWR0aDo2NDBweCIgcm9sZT0iaW1nIiBhcmlhLWxhYmVsPSJBIGJsdWUgcmFtcCBmcm9tIDUwIHRvIDkwMCBhbmQgYSBuZXV0cmFsIGdyZXkgcmFtcCBmcm9tIDUwIHRvIDkwMCwgZWFjaCBpbiB0ZW4gc3RlcHMiPgo8Zz4gPHJlY3QgeD0iMTYiIHk9IjgiIHdpZHRoPSI2MCIgaGVpZ2h0PSIyNCIgZmlsbD0iI2VmZjZmZiIgLz48cmVjdCB4PSI3OCIgeT0iOCIgd2lkdGg9IjYwIiBoZWlnaHQ9IjI0IiBmaWxsPSIjZGJlYWZlIiAvPiA8cmVjdCB4PSIxNDAiIHk9IjgiIHdpZHRoPSI2MCIgaGVpZ2h0PSIyNCIgZmlsbD0iI2JmZGJmZSIgLz48cmVjdCB4PSIyMDIiIHk9IjgiIHdpZHRoPSI2MCIgaGVpZ2h0PSIyNCIgZmlsbD0iIzkzYzVmZCIgLz4gPHJlY3QgeD0iMjY0IiB5PSI4IiB3aWR0aD0iNjAiIGhlaWdodD0iMjQiIGZpbGw9IiM2MGE1ZmEiIC8+PHJlY3QgeD0iMzI2IiB5PSI4IiB3aWR0aD0iNjAiIGhlaWdodD0iMjQiIGZpbGw9IiMzYjgyZjYiIC8+IDxyZWN0IHg9IjM4OCIgeT0iOCIgd2lkdGg9IjYwIiBoZWlnaHQ9IjI0IiBmaWxsPSIjMjU2M2ViIiAvPjxyZWN0IHg9IjQ1MCIgeT0iOCIgd2lkdGg9IjYwIiBoZWlnaHQ9IjI0IiBmaWxsPSIjMWQ0ZWQ4IiAvPiA8cmVjdCB4PSI1MTIiIHk9IjgiIHdpZHRoPSI2MCIgaGVpZ2h0PSIyNCIgZmlsbD0iIzFlNDBhZiIgLz48cmVjdCB4PSI1NzQiIHk9IjgiIHdpZHRoPSI1MCIgaGVpZ2h0PSIyNCIgZmlsbD0iIzE3MjU1NCIgLz4gPHJlY3QgeD0iMTYiIHk9IjQwIiB3aWR0aD0iNjAiIGhlaWdodD0iMjQiIGZpbGw9IiNmOGZhZmMiIC8+PHJlY3QgeD0iNzgiIHk9IjQwIiB3aWR0aD0iNjAiIGhlaWdodD0iMjQiIGZpbGw9IiNmMWY1ZjkiIC8+IDxyZWN0IHg9IjE0MCIgeT0iNDAiIHdpZHRoPSI2MCIgaGVpZ2h0PSIyNCIgZmlsbD0iI2UyZThmMCIgLz48cmVjdCB4PSIyMDIiIHk9IjQwIiB3aWR0aD0iNjAiIGhlaWdodD0iMjQiIGZpbGw9IiNjYmQ1ZTEiIC8+IDxyZWN0IHg9IjI2NCIgeT0iNDAiIHdpZHRoPSI2MCIgaGVpZ2h0PSIyNCIgZmlsbD0iIzk0YTNiOCIgLz48cmVjdCB4PSIzMjYiIHk9IjQwIiB3aWR0aD0iNjAiIGhlaWdodD0iMjQiIGZpbGw9IiM2NDc0OGIiIC8+IDxyZWN0IHg9IjM4OCIgeT0iNDAiIHdpZHRoPSI2MCIgaGVpZ2h0PSIyNCIgZmlsbD0iIzQ3NTU2OSIgLz48cmVjdCB4PSI0NTAiIHk9IjQwIiB3aWR0aD0iNjAiIGhlaWdodD0iMjQiIGZpbGw9IiMzMzQxNTUiIC8+IDxyZWN0IHg9IjUxMiIgeT0iNDAiIHdpZHRoPSI2MCIgaGVpZ2h0PSIyNCIgZmlsbD0iIzFlMjkzYiIgLz48cmVjdCB4PSI1NzQiIHk9IjQwIiB3aWR0aD0iNTAiIGhlaWdodD0iMjQiIGZpbGw9IiMwZjE3MmEiIC8+IDxnIGZvbnQtc2l6ZT0iOSIgZmlsbD0iY3VycmVudENvbG9yIiBmaWxsLW9wYWNpdHk9Ii43Ij4gPHRleHQgeD0iMTYiIHk9IjYiPjUwPC90ZXh0Pjx0ZXh0IHg9IjMyNiIgeT0iNiI+NTAwPC90ZXh0Pjx0ZXh0IHg9IjU3NCIgeT0iNiI+OTUwPC90ZXh0PiA8L2c+IDwvZz4KPC9zdmc+)

**Use a perceptual colour space for the maths.** HSL lies about lightness: `hsl(60 100% 50%)` (yellow) and `hsl(240 100% 50%)` (blue) claim the same 50 percent and are wildly different to the eye. OKLCH fixes this, so a ramp built in OKLCH has steps that actually look evenly spaced, and two hues at the same lightness really match.

``` css
:root {
  /* lightness, chroma, hue: evenly stepped and predictable */
  --accent-400: oklch(70% 0.14 250);
  --accent-500: oklch(62% 0.16 250);
  --accent-600: oklch(54% 0.17 250);
}
```

**Colour must never be the only carrier of meaning.** Roughly 1 in 12 men has a colour vision deficiency, and red-green is the common one, which is exactly the pair most status indicators use. Add an icon, a shape, a label or a pattern. This is a WCAG requirement and it is also just better design, since it survives a greyscale printout and a bright afternoon on a phone. Details in [Accessibility](../UI_UX/accessibility.llms.md).

**Contrast minimums** (WCAG 2.2 AA): 4.5:1 for normal text, 3:1 for text at 24 px or 19 px bold and above, 3:1 for the visible boundary of interactive components and meaningful graphics. Check with a contrast tool rather than by eye, since eye judgement of contrast is unreliable.

**Design light and dark together, not dark as an afterthought.** Dark mode is not inverted light mode. Saturated colours vibrate on dark grounds and need to be desaturated; pure black backgrounds with pure white text produce halation, so use a very dark grey with a slightly dimmed white; and shadows stop working as elevation cues, so depth has to come from surface lightness instead. Tokens make this a table of values rather than a second stylesheet, which is the subject of the next notebook.

------------------------------------------------------------------------

## 6. Gestalt principles

The rules by which the visual system groups things before conscious reading. Five of them matter daily.

![](data:image/svg+xml;base64,PHN2ZyB2aWV3Ym94PSIwIDAgNjQwIDExMCIgd2lkdGg9IjEwMCUiIHN0eWxlPSJtYXgtd2lkdGg6NjQwcHgiIHJvbGU9ImltZyIgYXJpYS1sYWJlbD0iRGlhZ3JhbXMgb2YgcHJveGltaXR5LCBzaW1pbGFyaXR5LCBjb21tb24gcmVnaW9uLCBjb250aW51aXR5IGFuZCBjbG9zdXJlIj4KPGcgZmlsbD0iY3VycmVudENvbG9yIj4gPGc+PGNpcmNsZSBjeD0iMjQiIGN5PSI0NiIgcj0iNSI+PC9jaXJjbGU+PGNpcmNsZSBjeD0iNDAiIGN5PSI0NiIgcj0iNSI+PC9jaXJjbGU+PGNpcmNsZSBjeD0iNzQiIGN5PSI0NiIgcj0iNSI+PC9jaXJjbGU+PGNpcmNsZSBjeD0iOTAiIGN5PSI0NiIgcj0iNSI+PC9jaXJjbGU+IDx0ZXh0IHg9IjI0IiB5PSI4MCIgZm9udC1zaXplPSI5IiBmaWxsLW9wYWNpdHk9Ii43Ij5Qcm94aW1pdHk8L3RleHQ+PC9nPiA8Zz48Y2lyY2xlIGN4PSIxNTAiIGN5PSI0NiIgcj0iNSI+PC9jaXJjbGU+PHJlY3QgeD0iMTY3IiB5PSI0MSIgd2lkdGg9IjEwIiBoZWlnaHQ9IjEwIiAvPjxjaXJjbGUgY3g9IjE5NiIgY3k9IjQ2IiByPSI1Ij48L2NpcmNsZT48cmVjdCB4PSIyMTMiIHk9IjQxIiB3aWR0aD0iMTAiIGhlaWdodD0iMTAiIC8+IDx0ZXh0IHg9IjE1MCIgeT0iODAiIGZvbnQtc2l6ZT0iOSIgZmlsbC1vcGFjaXR5PSIuNyI+U2ltaWxhcml0eTwvdGV4dD48L2c+IDxnPjxyZWN0IHg9IjI3MiIgeT0iMjYiIHdpZHRoPSI3NiIgaGVpZ2h0PSI0MCIgcng9IjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iY3VycmVudENvbG9yIiBzdHJva2Utb3BhY2l0eT0iLjUiIC8+IDxjaXJjbGUgY3g9IjI5MiIgY3k9IjQ2IiByPSI1Ij48L2NpcmNsZT48Y2lyY2xlIGN4PSIzMTAiIGN5PSI0NiIgcj0iNSI+PC9jaXJjbGU+PGNpcmNsZSBjeD0iMzI4IiBjeT0iNDYiIHI9IjUiPjwvY2lyY2xlPiA8dGV4dCB4PSIyNzIiIHk9IjgwIiBmb250LXNpemU9IjkiIGZpbGwtb3BhY2l0eT0iLjciPkNvbW1vbiByZWdpb248L3RleHQ+PC9nPiA8Zz48cGF0aCBkPSJNNDAwIDYyIEMgNDIwIDI2LCA0NDggMjYsIDQ2OCA2MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJjdXJyZW50Q29sb3IiIHN0cm9rZS1vcGFjaXR5PSIuNiIgLz4gPGNpcmNsZSBjeD0iNDAwIiBjeT0iNjIiIHI9IjMiPjwvY2lyY2xlPjxjaXJjbGUgY3g9IjQzNCIgY3k9IjM0IiByPSIzIj48L2NpcmNsZT48Y2lyY2xlIGN4PSI0NjgiIGN5PSI2MiIgcj0iMyI+PC9jaXJjbGU+IDx0ZXh0IHg9IjQwMCIgeT0iODAiIGZvbnQtc2l6ZT0iOSIgZmlsbC1vcGFjaXR5PSIuNyI+Q29udGludWl0eTwvdGV4dD48L2c+IDxnPjxwYXRoIGQ9Ik01NDAgMjggQSAyMiAyMiAwIDEgMSA1NDAgNjgiIGZpbGw9Im5vbmUiIHN0cm9rZT0iY3VycmVudENvbG9yIiBzdHJva2Utb3BhY2l0eT0iLjYiIHN0cm9rZS13aWR0aD0iMiIgLz4gPHRleHQgeD0iNTI0IiB5PSI4MCIgZm9udC1zaXplPSI5IiBmaWxsLW9wYWNpdHk9Ii43Ij5DbG9zdXJlPC90ZXh0PjwvZz4gPC9nPgo8L3N2Zz4=)

| Principle | Statement | Interface use |
|----|----|----|
| **Proximity** | Near things are related | The primary grouping tool. See section 3 |
| **Similarity** | Alike things are related | Same styling implies same kind. So do not style two different kinds identically |
| **Common region** | A shared enclosure groups | Cards and panels. Weaker than proximity, so do not rely on a border to fix bad spacing |
| **Continuity** | The eye follows a line | Alignment along an edge creates an implied path down the page |
| **Closure** | The eye completes a shape | Why a partly visible row communicates “scroll for more” |

Two corollaries worth stating outright:

- **Similarity cuts both ways.** If two elements look the same, users will expect them to behave the same. A clickable card next to a non-clickable card in the same style is a design bug, not a user error.
- **Proximity beats a border.** When spacing and enclosure disagree, spacing wins. That is why a form with even spacing inside a box is still ambiguous.

------------------------------------------------------------------------

## 7. Elevation, depth and borders

Depth answers “what is on top of what”, which matters for menus, dialogs, sticky headers and drag operations.

**Three tools, in order of subtlety:** background lightness, border, shadow. Use the least that works.

``` css
:root {
  --shadow-1: 0 1px 2px rgb(0 0 0 / .06);                        /* resting card    */
  --shadow-2: 0 2px 8px rgb(0 0 0 / .08);                        /* hovered, raised */
  --shadow-3: 0 8px 24px rgb(0 0 0 / .12);                       /* dropdown        */
  --shadow-4: 0 16px 48px rgb(0 0 0 / .18);                      /* modal           */
}
```

**Keep a consistent light source.** If one shadow is offset downward, all of them are. Mixed shadow directions read as sloppiness even to people who cannot say why.

**A shadow is a semantic signal, not a decoration.** Reserve the deeper levels for things that genuinely float and are dismissible. A static card with a modal-sized shadow makes the whole hierarchy unreadable.

**Elevation does not translate to dark mode.** A black shadow on a near-black surface is invisible, so depth in dark themes comes from making the raised surface lighter than its ground. That is one more reason to express elevation as a token with a per-theme value rather than a hard-coded shadow.

**Prefer a border to a shadow for anything static**, and prefer a background change to a border where you can get away with it. Borders at full strength box the page in; a border at low contrast (a neutral-200 rather than neutral-400) separates without shouting.

------------------------------------------------------------------------

## 8. Icons

Icons are a compression format. They save space and speed recognition for concepts the user already knows, and they hide functionality for everything else.

- **Use one icon set.** Mixed stroke weights and corner radii between sets are immediately visible and look like a mistake. Pick one (Lucide, Phosphor, Material Symbols, Heroicons) and stay in it.
- **Label anything ambiguous.** Only a handful of icons are genuinely universal: close, search, print, plus a few platform conventions. A three-dot menu, a bookmark, a share glyph and anything domain-specific need words. Icon-only toolbars are a recognised usability problem, not a modern aesthetic.
- **If it must be icon-only, give it an accessible name and a tooltip.** `aria-label` for assistive technology and a visible tooltip on hover and focus for everyone else.
- **Match the optical size to the text**, typically 1 em to 1.25 em beside body text, and align to the cap height rather than the line box.
- **Prefer inline SVG** for anything that must inherit colour or change with state. `currentColor` makes an icon follow its text automatically, which is why every SVG in this notebook uses it.
- **Decorative icons get `aria-hidden="true"`**, so a screen reader does not announce a meaningless graphic next to the label it duplicates.

``` html
<!-- Icon plus text: the icon is decorative, the text is the name -->
<button><svg aria-hidden="true" width="16" height="16">...</svg> Delete site</button>

<!-- Icon only: the icon must carry the name -->
<button aria-label="Delete site" title="Delete site"><svg aria-hidden="true">...</svg></button>
```

[SVG](../svgs.llms.md) covers the format itself in depth.

------------------------------------------------------------------------

## 9. How visual design fails

- **No hierarchy.** Everything at 14 px in the same grey. Squint at the screen and nothing emerges.
- **Too many type sizes and weights**, usually because each screen was designed alone. Six sizes that differ by 1 px each communicate less than three that differ clearly.
- **Arbitrary spacing.** 13 px here, 18 px there, and grouping that has to be rescued with borders.
- **Colour as decoration.** Accent colour on six elements, so the primary action no longer stands out.
- **Colour as the only signal.** Red and green status dots with no icon or label.
- **Contrast traded for aesthetics.** Light grey placeholder text on white is the most common accessibility failure in visual design, and it fails for everyone on a phone outdoors, not only for people with low vision.
- **Shadows everywhere.** When every element floats, nothing does.
- **Centred body text**, which forces the eye to find a new left edge on every line.
- **Full-width text on a large monitor.** A 200-character line is unreadable no matter how good the type is.
- **Dark mode by inversion**, producing vibrating saturated colours and invisible elevation.

------------------------------------------------------------------------

## Where this goes next

- [Design Systems and Tokens](../UI_UX/design_systems_and_tokens.llms.md) turns every scale in this notebook into named values a whole team can use, and is how light and dark stay in step.
- [Responsive and Multiplatform](../UI_UX/responsive_and_multiplatform.llms.md) covers how these layouts behave as the viewport changes.
- [Accessibility](../UI_UX/accessibility.llms.md) holds the contrast requirements, target sizes and colour independence rules this notebook keeps pointing at.
- [Content Design and Motion](../UI_UX/content_design_and_motion.llms.md) covers the words inside the hierarchy.

On the implementation side: [CSS](../css.llms.md) for the properties, [Bootstrap](../bootstrap.llms.md) for a ready-made grid and component set, and [SVG](../svgs.llms.md) for vector assets and icons.

------------------------------------------------------------------------

Back to top
