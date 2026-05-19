# Component Libraries

Synthesised from the foundational frontend skills, with attention to the most common React component ecosystems: shadcn/ui, Radix, Headless UI, MUI, Mantine, Chakra, and Ant Design.

Component libraries are accelerators. Used well, they give you a head start on a coherent design system. Used poorly, they make your product look like every other product using the same library.

## Core positions

1. **Libraries are starting points, not finishes.** A site that looks like an unmodified library default is forgettable. Reskin and recompose.
2. **The library's primitives are valuable; the library's defaults are negotiable.** Adopt the accessibility, keyboard handling, and state machinery; reject the visual defaults.
3. **One library, not three.** Mixing MUI + shadcn + custom is incoherent and bloats bundles. Pick one and commit.
4. **The library's design language is in its tokens.** Reskinning means rewiring tokens (colour, spacing, type, radius) before touching component code.
5. **Some primitives are not worth replacing.** Date pickers, combo boxes, drag-and-drop, complex menus. Use the library; restyle aggressively.

## The library landscape (2026 snapshot)

- **shadcn/ui** — copy-paste Radix-based components into your repo. Maximum control, no runtime dependency. The dominant choice for tailored apps.
- **Radix Primitives** — unstyled accessibility primitives. The foundation under shadcn. Use directly when shadcn's compositions don't fit.
- **Headless UI** — Tailwind Labs' unstyled primitives. Similar to Radix; smaller surface, tightly Tailwind-aligned.
- **MUI** — opinionated Material design implementation. Strong for products that want Material's visual language, frustrating to escape from.
- **Mantine** — opinionated but pragmatic; rich component set; easier to restyle than MUI.
- **Chakra UI** — flexible, design-system-friendly; declining momentum vs shadcn.
- **Ant Design** — enterprise-leaning, dense, distinctive. Strong for B2B / admin tools.
- **Park UI / NextUI / Catalyst** — newer entrants, varying maturity.

## shadcn/ui

Because it's the dominant choice, deeper notes:

- **Components are copied into your repo**, not installed as a package. Edit freely.
- **Built on Radix** for accessibility primitives + Tailwind for styling.
- **Token system** lives in `app/globals.css` as CSS custom properties on `:root` and `.dark`.

**Reskinning shadcn:**

1. **Replace the colour tokens.** Default shadcn uses HSL custom properties (`--background`, `--foreground`, `--primary`, etc.). Replace with your brand palette. This single change shifts the product 80% away from generic shadcn.
2. **Pick a non-default font.** Shadcn ships Inter by default. Inter is fine; it's also everywhere. A different sans (or a serif) immediately changes the product's character.
3. **Adjust the radius.** `--radius: 0.5rem` is the default; sharper (`0.25rem`, `0`) or softer (`0.75rem`, `1rem`) shifts feel substantially.
4. **Modify component spacings.** Shadcn buttons are `h-10 px-4`. Adjust per your spacing/density philosophy.
5. **Custom typography** in `tailwind.config.js` or `@theme`: replace default font sizes with your scale; add letter-spacing and line-height tokens.
6. **Edit individual components.** Open `components/ui/button.tsx`; modify variants. The point of shadcn is this is *your code*.

**What shadcn is good for:**
- Accessible, sensible buttons, inputs, tabs, dialogs, popovers.
- Date pickers, comboboxes (via `cmdk`), drag-and-drop bases.
- Data tables (via TanStack Table integration).

**What shadcn is not the answer for:**
- Hero sections, landing pages. Build those bespoke.
- Editorial typography. Roll your own.
- Distinctive product chrome (custom nav, custom workflow surfaces).

## Radix Primitives (direct)

When shadcn's composition doesn't fit, drop down to Radix:

```tsx
import * as Popover from '@radix-ui/react-popover';

<Popover.Root>
  <Popover.Trigger asChild>
    <button>Open</button>
  </Popover.Trigger>
  <Popover.Portal>
    <Popover.Content className="...">
      ...
    </Popover.Content>
  </Popover.Portal>
</Popover.Root>
```

Radix gives you: ARIA roles, keyboard navigation, focus management, portal rendering, controlled / uncontrolled state. You add: visual style.

## Headless UI

Tailwind Labs' alternative to Radix. Tightly integrated with Tailwind's transition utilities. Smaller component set than Radix but tracks Tailwind's idioms.

## MUI

Strong if you want Material; painful otherwise.

- **Theme override** via `createTheme()` — re-skin colours, typography, spacing.
- **`styled()`** for per-component overrides.
- **MUI's surface is distinctive.** A "reskinned MUI" still reads as MUI to trained eyes. Embrace it or pick a different library.
- **Bundle size**: MUI is heavy. Consider the cost.

## Mantine

A pragmatic middle ground: many components, easier to restyle than MUI, less granular than shadcn.

- **CSS variables theme** for tokens.
- **Component-level style overrides** via `styles` and `classNames` props.
- **Good for dashboards** and admin interfaces that need range without bespoke building.

## Common anti-patterns

- **Shipping default-themed shadcn.** Looks like every other shadcn site. Reskin tokens before launching.
- **Mixing libraries.** shadcn for buttons + MUI for tables + custom for everything else is incoherent.
- **Using a library because it has many components.** A library used for 3 components is fine; one used for 30 components ties you to its design language whether you like it or not.
- **Building bespoke when a library exists.** Date pickers, comboboxes, drag-and-drop are deep rabbit holes. Use the library.
- **Fighting the library's accessibility.** If Radix focus-traps a dialog and you "fix" it because focus is annoying, you've broken keyboard access.

## Picking a library

Ask:

- **Do you need fine control over visuals?** Yes → shadcn / Radix directly. No → Mantine / MUI.
- **Do you have time to invest in reskinning?** Yes → shadcn. No → Mantine.
- **Is the product brand-led or function-led?** Brand-led → custom built on Radix. Function-led → opinionated library is fine.
- **What's the team's Tailwind comfort?** High → shadcn or Headless UI. Low → Mantine, MUI, or Chakra.
- **Is bundle size critical?** Yes → shadcn (copies only what you use). No → MUI/Mantine fine.

## Migrating between libraries

Migrations are expensive. Plan:

- **Component-by-component**, not big-bang. Keep both libraries during migration; remove the old gradually.
- **Wrap before swap**. Create a project-local `<Button>` that delegates to the current library; swap implementations behind it.
- **Visual regression tests** (Chromatic, Percy, Playwright snapshots) before and after.

## What to verify before declaring component-library work done

- Have you reskinned tokens away from the library's defaults?
- Is the product visually distinct from sites using the same library unmodified?
- Is exactly one library in use, not two or three?
- Are accessibility primitives intact (focus management, ARIA, keyboard)?
- Are you using the library for components that are worth using, and building bespoke for the rest?
- Have you audited bundle size against your budget?
