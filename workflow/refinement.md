# Refinement

How to take a surface from "working" to "done". Synthesised from the polish-oriented patterns in the foundational frontend skills and the editorial discipline of repeated revision.

Refinement is the work most often skipped. The functional version is in production; the refined version is what people remember.

## Core positions

1. **Working is not done.** A surface that ships its primary task is the *starting point* of refinement, not the conclusion.
2. **Refinement is mostly subtraction.** Most refinement passes remove or quieten elements rather than add them. If your refinement pass *adds* features, you're not refining, you're scoping.
3. **Pass discipline matters.** Refinement happens in passes (typography, spacing, motion, copy) not all at once. Trying to fix everything simultaneously produces half-fixes everywhere.
4. **Time-boxed refinement.** Polish without a budget becomes infinite. Allocate the time, do the most important passes first, ship.
5. **The user doesn't see your refinement, only its absence.** When refinement is done well, the page just feels *right*. When it's missing, the user feels something is off without being able to name it.

## When to refine

- **Before a major release** — gate it on a refinement pass.
- **After a feature lands** — the next iteration after MVP.
- **When the work feels off** — your gut is right; investigate.
- **Periodically across the product** — drift accumulates. Sweep through pages.

Don't refine *during* initial build; you'll never ship. Build to "working", then refine.

## The audit-first protocol

Before changing anything, audit the surface. Produce a list, not edits.

For each problem area you spot, classify:

- **Must** — clearly wrong, breaks the work. Examples: a button that doesn't show focus, copy with a typo, a state that's missing.
- **Should** — a clear improvement, worth the cost. Examples: tightening display letter-spacing, swapping `ease-in-out` for `ease-out` on entry motion, replacing a stock icon with a custom one.
- **Could** — small refinements at the edge of perception. Examples: 1px shadow tweak, slightly tighter line-height, a slightly off-pure-black foreground.
- **Don't** — patterns to remove rather than improve. Examples: the third nested gradient on the hero, the decorative animation behind a paragraph, the "Built with X" footer.

Present the list. Get alignment (from yourself, from the team, from the stakeholder) on which tier of items to address. *Then* edit.

The reason: refinement passes have momentum and can balloon. The audit-first protocol prevents one "fix the spacing" task from becoming a three-day rewrite.

## Common refinement passes

### Typography pass

- Limit the type scale. If you have 12 sizes in use, reduce to 7.
- Limit the weights. If you have 5 weights and 2 italics in use, reduce.
- Tighten display letter-spacing.
- Adjust line-height per size.
- Enable tabular numbers in tables and lists with numbers.
- Replace `font-style: italic` synthetic obliques with actual italic font files.

### Spacing pass

- Move every off-scale value to the scale.
- Audit outer-padding vs inner-gap (outer should be ≥ inner).
- Promote macro whitespace where the page feels cramped.
- Demote micro whitespace where the page feels stretched.

### Motion pass

- Audit every animation against "why is this moving?"
- Replace `transition: all` with property-specific transitions.
- Replace `ease-in-out` with role-appropriate easings.
- Reduce durations that drag.
- Remove decorative motion.

### Copy pass

- Read every UI string aloud. Does it sound human?
- Remove em dashes.
- Remove "Awesome!", "Great!", "Let's go!" enthusiasm.
- Make button labels verbs.
- Make error messages specific and actionable.
- Remove "Built with", "Powered by", "Trusted by" unless genuinely earned.

### Colour pass

- Reduce accent count to one.
- Re-derive dark mode rather than inverting.
- Audit contrast at body and at metadata levels.
- Replace pure #000 / pure #FFF with refined alternatives.

### State pass

- Implement missing states (loading, empty, partial, error, success).
- Audit interactive elements for hover, focus, active, disabled.
- Test empty states by actually emptying the data.
- Test error states by actually breaking the network.

### Detail pass

- 1-2px alignment fixes that read as off without being noticed.
- Hairline borders where shadows aren't doing enough.
- Icon weight matched to type weight.
- Hover states that don't shift layout.
- Focus rings visible in all contexts.
- Hung punctuation on display type.

## What refinement is not

- **Not adding features.** That's scope.
- **Not rebuilding from scratch.** That's redesign.
- **Not chasing trends.** That's drift.
- **Not asking the team's opinion on every detail.** That's design-by-committee.

## Restraint

Refinement is easy to over-do. Signs you've gone too far:

- You've spent a full day on a single section.
- You can't articulate what you've changed; the diff is a chaos of micro-tweaks.
- The site looks subtly *worse* than before because too many things shifted at once.
- You've added more than you've removed.

When in doubt, revert and pick one thing to fix.

## The 80/20 of refinement

Most surfaces hit 80% of "done" via:

1. Limiting the type scale.
2. Limiting the accent count to one.
3. Removing 30% of the elements (decorative motion, redundant icons, dead UI).
4. Fixing the missing states.
5. Reading the copy aloud and rewriting the weakest 3 strings.

If time is short, do these five things and stop. The remaining 20% takes 80% of the time and is invisible to most users.

## What to verify before declaring refinement done

- Did you audit before editing?
- Did you classify items by Must / Should / Could / Don't?
- Did you address all Musts?
- Did you address Shoulds proportional to budget?
- Did you remove at least as much as you added?
- Does the surface read as *quiet and confident* rather than *busy and trying*?
- Have you walked away and come back?
- Have you tested in browser, on mobile, at 200% zoom, with reduced motion, with keyboard only?

If yes to all, the work is done.
