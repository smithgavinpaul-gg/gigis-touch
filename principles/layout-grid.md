# Layout & Grid

Synthesised from the foundational design skills and the layout discipline embedded in editorial / brutalist / modernist design traditions.

Layout is the spatial logic that holds the rest of the design together. Without a grid, every other decision floats.

## Core positions

1. **The grid is invisible but felt.** Users do not see the grid; they feel its absence as "off". Establish a grid before placing the first element.
2. **Asymmetry beats centred symmetry for serious work.** Centred-everything layouts read as templated or ceremonial. Asymmetric layouts read as designed.
3. **Whitespace is the design.** The space *around* elements does more communicative work than the elements themselves. Treat it as a primary tool, not a leftover.
4. **Hierarchy is spatial.** Position is one of the strongest hierarchy signals. Where something sits on the page tells the reader how to weight it before they read the content.
5. **Responsive is not breakpoints alone.** Responsive design is a *content order*, a *navigation strategy*, and a *touch-target strategy*, with breakpoints as the visible tool.

## Grid systems

The standard grids and their characters:

- **12-column** — the universal default. Subdivides into 2, 3, 4, 6 column layouts cleanly. Best for marketing, product, and dashboards.
- **8-column** — denser, suits editorial work and tools with a fixed sidebar.
- **6-column** — clearer divisions, suits long-form and asymmetric editorial layouts.
- **4-column** — mobile-native, also a strong choice for minimalist desktop layouts.
- **No grid, deliberate placement** — only for hero or art-directed sections. Even these should sit *on* an invisible baseline.

Gutters between columns: usually 16-32px depending on density. Outer page margins: at least 2× the gutter on desktop, full bleed only when intentional.

## Spacing scale

Pick one and only use values from it.

- **4px scale**: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128. Tailwind default.
- **8px scale**: 8, 16, 24, 32, 48, 64, 96, 128. Looser, suits mobile-first.
- **Golden ratio scale**: 8, 13, 21, 34, 55, 89. Suits editorial.

Pixel values outside the scale are smells. If you find yourself reaching for an off-scale value, ask whether the scale is wrong or your judgement is.

## Whitespace

- **Macro whitespace** (margins, section spacing): defines breathing room. Generous macro whitespace is the single biggest "premium" signal in digital design.
- **Micro whitespace** (padding, gaps): defines grouping. Related items closer, unrelated items further (proximity principle).
- **Outer padding ≥ inner gap.** A container's padding should be at least as large as the gap between its children. Reversed, it looks broken.
- **The blank page is the goal, not the starting point.** Begin a layout by deciding what *not* to include. Then add only what serves a task.

## Hierarchy through position

In LTR cultures, the eye lands roughly in the upper-left, then sweeps right and down. Use this:

- **Top of the page** = orientation. Logo, primary nav, page title.
- **First fold** = the primary message and primary action.
- **Below the fold** = supporting content, in decreasing priority.
- **Visual centre** ≠ geometric centre. The visual centre sits slightly above the geometric centre. Important elements that need to feel "centred" should sit at the visual centre.

## Asymmetry and rhythm

- A purely symmetric layout reads as static. A purely asymmetric layout reads as chaotic. Most strong layouts have *one* major asymmetric move and a series of locally symmetric details.
- The rule of thirds applies: place the dominant element on a third-line, not the centre, for visual interest.
- Establish a vertical rhythm: section spacings derived from a baseline unit so the page has a felt cadence.
- Hang punctuation. Opening quotes, dashes, periods hang outside the column edge for optical alignment.

## Edge-bleed

- **Type that bleeds off the edge** reads as confident editorial. Use it once or twice per long page, never on the primary headline.
- **Imagery that bleeds full-width** reads as cinematic. Use deliberately; full-width imagery interrupts reading flow.
- **Boxed-in everything** reads as a template. Some elements *should* break the box.

## Responsive logic

- **Content-first responsive**: decide the content priority order before deciding breakpoints. What is the *most* important thing on mobile? It should be the first thing visible.
- **Touch targets** on mobile: 44×44px minimum (iOS), 48×48dp (Android). Spacing between touch targets at least 8px.
- **Type re-scales**, layout re-flows, navigation reformats. All three change, not just one.
- **Breakpoints derive from content, not devices.** If your content needs 3 columns to read well, your breakpoint is where 3 columns stop working, not at iPad-width.
- **Use container queries** where supported. A component should respond to its container, not the viewport.

## Common breakpoints (starting points)

- 0-639px: mobile portrait. Single column, stacked nav, full-width touch targets.
- 640-1023px: mobile landscape and tablet portrait. Possibly two columns, possibly still single.
- 1024-1279px: tablet landscape and small desktop. Multi-column begins, sidebar nav viable.
- 1280-1535px: desktop. Full grid in use.
- 1536px+: large desktop. Don't expand the content; use the extra space for whitespace or sidebars.

Tune to the content. A reading-focused site might cap content at 720px even at 1920px viewport.

## Navigation patterns

- **Top nav** for marketing, content sites, simple tools. 5-7 items max.
- **Sidebar nav** for products with many sections (dashboards, settings-heavy apps). 7-20 items, possibly with sub-grouping.
- **Bottom tab bar** for mobile apps. 3-5 items, with the primary action sometimes in the centre as a raised button.
- **Command palette** (Cmd-K) as a power-user accelerator on top of any of the above. Should not be the *only* way to find things.

## Long-form layouts

- Single column at 640-720px max for prose.
- Margin notes / footnotes in a side gutter at 50-60% body width on desktop, collapsing inline on mobile.
- Section breaks visible: extra whitespace, ornaments, or rules.
- Continuous scrolling beats paginated for most reading; paginated wins for very long structured documents.

## Dashboard layouts

- Most important metric at top-left.
- Comparable metrics in a row, same shape, same scale.
- Charts and tables aligned to the same grid as everything else.
- Filters and controls anchored consistently (usually top or left), not scattered.

## What to verify before declaring layout done

- Is there an explicit grid (column count, gutter, margin) in use?
- Are all spacing values from a single scale?
- Is outer padding at least equal to inner gap?
- Does the page have one dominant element per fold, not three?
- At 320px viewport, does the layout still work?
- At 1920px viewport, has the content been prevented from sprawling?
- Have you tested the focus order against the visual order?
- Has every centred element been re-evaluated for whether asymmetric would be stronger?
