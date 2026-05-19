# User Interface

Synthesised from the UI-oriented skills (`LibreUIUX-Claude-Code`, `interface-design`, `claude-design-skill`, `frontend-design` foundational set).

UI is the discipline of turning a clear task flow into a clear visual surface. UX decides *what is on the screen*; UI decides *how that thing reads*.

## Core positions

1. **Hierarchy is the single most important UI skill.** A user should know within a glance: what is this page, what is the action, what is content, what is metadata. Every other UI decision is downstream.
2. **Affordance: things should look like what they do.** A button should look pressable, an input should look writable, a link should look followable. The current era has eroded this; resist the erosion.
3. **Feedback: every interaction must respond.** A click without feedback feels broken. A submit without acknowledgement feels lost. The feedback can be small, but it must exist.
4. **Density is a choice, not a default.** A trading terminal needs density; a meditation app needs space. Pick the density for the user's situation, then commit.
5. **Components are a contract.** If a button looks one way here and another way there, you do not have a button, you have two buttons pretending to be one.

## Visual hierarchy

Hierarchy is produced by *contrast*. Contrast in:

- **Size** — the largest thing reads first.
- **Weight** — heavier reads as more important.
- **Colour** — brighter or higher-contrast colour reads first.
- **Spacing** — more whitespace around an element promotes it.
- **Position** — top-left and visual centre read first (in LTR contexts).

Use these *in combination*, but not all at once. A title needs only two of these (e.g. larger + heavier) to be obviously a title. Stacking all five produces noise.

## Spacing

- **A scale, not freeform.** Pick a spacing scale (4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96, or the Tailwind default) and use only values from it. Freeform pixel values are a smell.
- **Related items closer, unrelated items further.** This is the gestalt principle of proximity, the cheapest grouping mechanism available.
- **Outer padding ≥ inner gap.** A card with 8px outer padding and 16px gap between items looks broken. The container should breathe more than its contents.
- **Vertical rhythm.** Section spacing should be derived from a baseline unit, not picked per section.

## Components

- **States, not just defaults.** Every interactive component has at least: default, hover, focus, active, disabled, loading. Some have selected, indeterminate, error. Design and implement all of them.
- **Naming is part of design.** A "Button" component should have a clear API (variant, size, leftIcon, rightIcon, isLoading, isDisabled). Bad component names produce bad call sites.
- **Composition over inheritance.** Build small components that compose, not one giant component with twenty boolean flags.
- **The system is recursive.** A button is a component. A button group is a component. A toolbar of button groups is a component. Each level has the same discipline: states, naming, composition.

## Controls

- **Buttons** carry weight by hierarchy: primary (one per page, the main action), secondary (alternatives), tertiary / ghost (utility), destructive (separate visual treatment). Never two primary buttons next to each other.
- **Links** for navigation, **buttons** for actions. Do not style buttons to look like links or vice versa.
- **Inputs** with persistent labels above (see `principles/ux.md`). Visible focus ring, never `outline: none` without replacement.
- **Toggles vs checkboxes**: toggle = instant effect, checkbox = will take effect on submit. They are not interchangeable.
- **Selects vs radios**: radios when there are 2-5 options and all should be visible, select when there are more or the choice is less central.

## Density and rhythm

- **Choose a base text size deliberately.** 14, 15, 16, or 18px are all defensible; the choice signals the product's character. Pick one and let the rest of the type scale derive from it.
- **Line-height is part of density.** Tight line-height (1.1-1.3) for display, comfortable (1.4-1.6) for body, looser (1.6-1.8) for long-form reading.
- **Component height should be quantised.** All buttons, inputs, and chips should share a height grid (32 / 36 / 40 / 48 px). Mixed heights in a row reads as accidental.
- **Don't centre everything.** Long-form reading benefits from left-aligned text. Centred text reads as marketing decoration past ~3 lines.

## Borders, fills, shadows

These are the three ways of separating a region from its background.

- **Borders** read as architectural and engineered. They suit information-dense interfaces, tools, and editorial work.
- **Fills** read as soft and grouped. They suit consumer interfaces, content apps, and warmth.
- **Shadows** read as floating and physical. They suit playful or skeuomorphic surfaces, and quickly look dated when overused.

Pick one as the dominant separator for the product, with the other two as occasional alternates. Mixing all three indecisively is a common AI-generic tell.

## Iconography

- **A library that fits the type weight.** Lucide is the safest default, but its 2px stroke can read thin against a heavy sans; bump to 2-2.5px or pick Heroicons solid for a heavier feel.
- **One library, one weight, one size grid.** Mixing icon libraries is a tell.
- **No icon is often the right answer.** A label does the work; an icon next to that label often becomes redundant. Icons earn their place when they replace text in tight spaces or aid scanability across a list.
- **Custom icons** for distinctive products, drawn to the brand's stroke and corner-radius personality.

## Cards, lists, tables

- **Cards** when items are heterogeneous or visually rich.
- **Lists** when items are homogeneous and the user scans top-to-bottom.
- **Tables** when items are comparable across structured columns. Real tables, with proper column alignment (text left, numbers right, currency right with consistent decimals).
- Do not turn a table into cards because cards "look modern". You lose scanability.

## What to verify before declaring UI done

- Is the primary action obvious within 1 second of seeing the screen?
- Does each interactive element have hover, focus, active, and disabled states?
- Are spacings drawn from a scale, or are there one-off pixel values?
- Is the type scale limited (5-8 sizes total), not freeform?
- Do components compose, or is each call site bespoke?
- If you blur your eyes, can you still see the hierarchy?
- Has the AI-generic fingerprint been audited out (see `principles/taste.md`)?
