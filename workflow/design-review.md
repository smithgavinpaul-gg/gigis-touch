# Design Review

A structured critique format for self-review or peer review. Synthesised from the review-oriented patterns in the source skills and the discipline of editorial / studio critique.

A design without review is incomplete. Review is the step where intent meets reality: does the work *actually do* what it claims to do?

## The protocol

Review in passes. Don't try to assess everything at once.

### Pass 1: Intent

Before looking at the surface, restate what the work is for.

- What is this surface supposed to accomplish?
- Who is it for?
- What is the primary action / primary content?

Then look at the work and ask: *does it look like what it says it is?*

- A settings page should look like a settings page. If it looks like a hero page, the intent is wrong.
- A reading page should look readable, not scannable.
- A tool should look usable, not promotional.

If intent and surface disagree, fix intent first.

### Pass 2: Hierarchy

Squint at the surface (or blur your eyes, or look at a low-resolution thumbnail).

- Can you tell what the page is about?
- Can you identify the primary action?
- Can you tell content from navigation from metadata?

If squinting destroys the hierarchy, the hierarchy isn't strong enough. The eye should land in the same place even with most detail removed.

### Pass 3: Typography

Read `principles/typography.md` if you need a reminder.

- Is the type scale limited (5-8 sizes, derived from a ratio)?
- Are weights limited (4-5 total)?
- Are line-lengths in the comfortable range (45-75ch for prose)?
- Is line-height appropriate to size?
- At display sizes, has letter-spacing been tightened?
- Are numerics tabular where they should be?

### Pass 4: Colour

Read `principles/color.md` if you need a reminder.

- Is there a single primary accent, or has it multiplied?
- Does body text pass contrast at AAA?
- Are status colours actually distinguishable (not just by hue)?
- In dark mode, has the palette been re-derived, not inverted?

### Pass 5: Layout & spacing

Read `principles/layout-grid.md` if you need a reminder.

- Is there an explicit grid?
- Are spacings on a scale, or are there one-off pixel values?
- Is outer padding ≥ inner gap?
- Is there a single dominant element per fold?
- Have you tested at 320px, 768px, 1280px, 1920px?

### Pass 6: Motion

Read `principles/motion.md` if you need a reminder.

- Does each animation answer "why is this moving?"
- Are durations role-appropriate?
- Are easings role-appropriate (ease-out for entry, ease-in for exit)?
- Is `prefers-reduced-motion` respected?
- Have you tested at 4× slow-down?

### Pass 7: States

For every interactive element:

- Default, hover, focus, active, disabled, loading. All implemented?
- For inputs: also error, valid, filled, focused-with-content.
- For lists / containers: also empty, partial, full, error.

Missing states are the most common UI failure.

### Pass 8: Copy

Read `principles/taste.md` and `principles/ux.md` if you need a reminder.

- Does the copy read as if a person wrote it, not a marketing team?
- Are button labels verbs, not nouns?
- Are error messages specific and actionable?
- Have em dashes been audited out of any AI-generated copy?
- Does the voice match the surface (clinical for tools, considered for editorial, energetic for marketing)?

### Pass 9: Accessibility

Read `principles/accessibility.md` if you need a reminder.

- Tab through the page. Does focus order match visual order? Is the focus ring visible?
- Run axe DevTools or Lighthouse. Critical issues?
- Test with a screen reader for at least one primary flow.
- Test at 200% browser zoom.
- Are touch targets 44×44px+ on mobile?

### Pass 10: AI-generic check

Read `principles/taste.md`'s fingerprint list.

- Is the work distinct from a default AI-generated equivalent?
- Are there any unintended generic patterns (purple gradients, rounded-2xl blob cards, three-column feature grids)?
- Could this design only be for this product, or could it be for any product?

If the answer to the last question is "any product", the work isn't done.

## Critique structure

When giving review to others (or to your own work in writing), use a structured format:

**Section 1: What's working.** Genuinely. Not flattery. Identify the strongest decisions in the work, the moves that landed.

**Section 2: What's at risk.** Decisions that might be wrong but where you're not sure. Frame as questions to explore: "Have you considered whether the centred layout suits the editorial weight of this section?"

**Section 3: What's broken.** Decisions that are clearly wrong. Frame as observations + recommendations: "The button hover state shifts the layout by 1px (cause: padding change on hover) — switch to a transform-based animation or a 1px transparent border."

**Section 4: What's missing.** Things the work should have but doesn't. Often the most valuable section.

Tiered priority:

- **Must** — blocks shipping. Accessibility violations, broken states, factual errors.
- **Should** — high-value improvements. Stronger hierarchy, better motion, sharper copy.
- **Could** — small refinements. Tighter letter-spacing on display, slightly more whitespace.
- **Don't** — patterns to remove. AI-generic tells, decorative motion, unused components.

## Self-review vs peer review

**Self-review** happens before showing to anyone. Use the protocol above. Be honest. The discipline is in catching your own mistakes before someone else does.

**Peer review** has different dynamics. The reviewer has fresh eyes; you have context. Don't dismiss reviewer comments by explaining context; if the reviewer needed the explanation, the design isn't explaining itself enough.

**Founder / client review** is yet another mode. They care about outcomes (does it sell, does it convert, does it feel premium) more than about details (kerning, motion easing). Translate detail-level feedback into outcome-level language when speaking to them.

## When to declare review done

- Every "must" item resolved.
- "Should" items either resolved, deferred with explicit reason, or dropped with explicit reason.
- "Could" and "don't" items addressed if time allows; documented for next iteration if not.
- The 10 passes above completed.
- A second pair of eyes has looked, even briefly.

If you're reviewing your own work and you can't find anything wrong, you're not looking hard enough. Walk away for 24 hours and come back. Distance is the cheapest critique tool.

## What to verify before declaring review complete

- Did you run all 10 passes?
- Did you check accessibility with a tool *and* with a keyboard?
- Did you test the work in at least 3 viewport widths?
- Did you audit copy for em dashes and AI-generic phrases?
- Did you walk away and come back at least once?
- Have you documented the "could" items for future iteration?
