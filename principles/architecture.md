# Architecture (Design-Side)

Synthesised from the software design skills (`claude-code-templates`, `code-architect` agent, `claude-code-ultimate-guide`, `claude-code-from-source`, `Dive-into-Claude-Code`) translated to the design-engineering boundary.

Design-side architecture is the discipline of *implementing* a design system so that the design holds together as the product grows. Without it, every new feature drifts further from the original direction until the system is a corpse.

## Core positions

1. **A design without architecture is a screenshot.** Designs that survive only as PNGs become inconsistent in code within a quarter. The architecture is what keeps the design alive.
2. **Tokens are the source of truth.** Every visible property should reference a token (colour, spacing, type, radius, shadow). Hard-coded values are leaks.
3. **Components are contracts, not snowflakes.** A `Button` is one thing with variants. Two `Button` components with slightly different APIs is a system that has already failed.
4. **The design-engineering boundary is a single layer.** Either designers work in code, or engineers work from a strict design source. A boundary that pretends to be both ends up being neither.
5. **Naming is architecture.** Bad component names produce bad call sites which produce bad design. Spend disproportionate time on naming.

## Token systems

Tokens are the design system's vocabulary. They have layers:

- **Primitive tokens** — raw values. `gray-50` = `#FAFAFA`, `space-4` = `16px`, `radius-md` = `8px`.
- **Semantic tokens** — meaning-bound. `text-primary`, `surface-elevated`, `border-default`. These reference primitive tokens but carry intent.
- **Component tokens** — specific to a component. `button-primary-bg` references `accent-default`. This layer is optional but useful in large systems.

Two-layer (primitive + semantic) is enough for most products. Three-layer (primitive + semantic + component) for design-system-heavy organisations.

## Naming tokens

- **Semantic, not visual.** `text-muted` beats `text-gray-500`. The latter locks you in.
- **Stable across themes.** A token's meaning should be the same in light and dark mode; the value changes.
- **Predictable shape.** Patterns like `{role}-{element}-{state}` (`button-primary-hover`) scale; ad-hoc names don't.
- **Avoid numbers without meaning.** `text-2` is opaque. `text-sm`, `text-md` is better.

## Tailwind-style token strategy

When using Tailwind, the `theme.extend` in `tailwind.config.js` (v3) or `@theme` in CSS (v4) is the token surface.

- **Override the colour palette** to your semantic tokens. Don't ship with default `indigo-500` references; replace with your own scale.
- **Limit fontFamily** to your chosen 1-2 families.
- **Extend spacing** only when necessary; the default Tailwind scale is well-considered.
- **Custom utilities** for things the design system reuses but Tailwind doesn't ship: e.g. a `prose-narrow` for editorial column widths.

## Component architecture

A component is well-architected when:

- **Single responsibility.** It does one thing visually and behaviourally.
- **Clear API.** Props are documented, named consistently, with sensible defaults. Boolean props read as positive (`isDisabled`, not `isEnabled`).
- **Composition over configuration.** Compound components (`Tabs.Root`, `Tabs.List`, `Tabs.Trigger`, `Tabs.Content`) scale better than monolithic ones (`<Tabs items={[...]} />`).
- **States explicit.** Hover, focus, active, disabled, loading, error, empty implemented per spec, not "we'll add them later".
- **Accessibility built in.** Focus management, keyboard handling, ARIA roles. Not an afterthought.
- **Composable with the rest of the system.** A button placed inside a card inside a modal should not need custom overrides to work.

## Component file structure

A pattern that scales (adapt to framework):

```
Button/
├── Button.tsx         # main component
├── Button.types.ts    # prop interfaces (optional, can co-locate)
├── Button.css         # local styles (or Tailwind in component)
├── Button.stories.tsx # Storybook or equivalent
├── Button.test.tsx    # tests
└── index.ts           # public exports
```

For smaller systems, a single file is fine. The principle: structure follows complexity.

## Variants and sizes

- **Define variants in code, not in markup.** A `<Button variant="primary">` is a contract; a `<button className="bg-blue text-white px-4 py-2 rounded">` repeated across the app is technical debt.
- **Variants for kind** (primary, secondary, ghost, destructive), **sizes for scale** (sm, md, lg). Two orthogonal dimensions.
- **Avoid boolean explosion.** `isPrimary + isLarge + isOutlined + isLoading + isDisabled` produces 32 combinations. Use enum-style variants.
- **`class-variance-authority` (cva)** or **`tailwind-variants` (tv)** are the modern way to express variant systems in Tailwind-based codebases.

## Composition primitives

A well-architected design system has primitives that compose. Common ones:

- **`<Stack>`** — vertical layout with consistent gap.
- **`<Cluster>`** — horizontal layout that wraps.
- **`<Grid>`** — explicit grid layout.
- **`<Spacer>` / `<Divider>`** — explicit space and rules.
- **`<Surface>`** — semantic surface with elevation.
- **`<Text>`** — type with semantic role (`<Text variant="display">`).

These primitives let designers compose layouts in JSX directly, without ad-hoc CSS.

## Design system as a package

For products with multiple surfaces (web, mobile, marketing, docs):

- **Single npm package** (`@company/ui`) exporting components, tokens, and utilities.
- **Versioned independently** from product code. Breaking changes get major bumps; product teams upgrade on their own schedule.
- **One source of truth for tokens**, exported as CSS variables, JS objects, and (where needed) iOS/Android assets.

Smaller products don't need a package; a `components/` directory is fine. Outgrow it deliberately.

## The design-engineering boundary

Two stable patterns; pick one and commit:

1. **Designers work in Figma, engineers translate.** The translation step is where drift happens. Mitigate with: a strict design token bridge (Tokens Studio, Style Dictionary), regular design-engineering pairing, and a "design implementation" review step.
2. **Designers work in code.** Either directly (designers write JSX/CSS) or via a sandbox (Storybook, prototype branches). Higher skill ceiling for the design team, lower drift.

The unstable third pattern is "Figma is the source of truth and engineers eyeball it". This works for the first sprint and breaks by the third.

## Documentation

- **Storybook (or equivalent)** for every component. Stories cover variants, sizes, and states.
- **Token reference** as a live page, not a PDF.
- **Usage guidelines** for non-obvious components: when to use a Tooltip vs a Popover, when a Drawer vs a Modal.
- **Examples beat specs.** A copy-pasteable code snippet teaches faster than a long description.

## Refactoring discipline

- **Don't refactor everything at once.** Big-bang design system migrations fail. Migrate component-by-component, with deprecation periods.
- **Codemods for token renames** where possible.
- **Visual regression testing** (Chromatic, Percy, Playwright snapshots) before and after.
- **Decisions logged.** When you remove a variant or rename a token, write down why.

## What to verify before declaring architecture done

- Are tokens defined and named semantically?
- Are colour, spacing, type, radius, and shadow all referenced via tokens, not hard-coded?
- Does every component have a clear API and states implemented?
- Is there a single source of truth for the design system?
- Are variant systems consistent (e.g. `variant + size`) across components?
- Is the design system documented somewhere call-site authors can reference?
- Does adding a new component fit a clear pattern rather than reinventing structure?
