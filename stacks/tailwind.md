# Tailwind CSS

Synthesised from the Tailwind-oriented skills (`claude-code-kit`, `secondsky/claude-skills`, `tailwindcss-marketplace`, `flyingwebie/claude-agents`, `sveltekit-svelte5-tailwind-skill`).

Tailwind is the dominant utility-first CSS framework. Used well, it accelerates a design system; used poorly, it produces incoherent class soup. The principles below apply to v3 and v4 unless noted.

## Core positions

1. **Tailwind is a token system with classes.** The classes are the surface; the underlying tokens are what make the system coherent. Configure the tokens (your colour palette, type scale, spacing) before writing any utility classes.
2. **Avoid arbitrary values.** `text-[#FF6A1F]`, `mt-[13px]`, `w-[437px]` are escape hatches. Each one is a token that should have been defined.
3. **Components beat repetition.** When you find yourself writing the same 6-class string in three places, extract a component. Tailwind is component-first, not utility-first.
4. **`@apply` sparingly.** It defeats the purpose of utilities (locality, atomicity). Use it only for genuinely cross-cutting concerns (typography defaults via `@apply` in a `prose` style).
5. **The framework is opinionated; honour the opinions.** The default spacing scale (4-based) and type scale work for most products. Customise the palette and fonts; leave the rest alone unless you have a specific reason.

## v3 vs v4 differences

**v3 (config-driven):**
- `tailwind.config.js` defines theme tokens.
- JIT mode compiles classes on demand.
- Config consumed via `theme()` function in CSS or JS.

**v4 (CSS-driven):**
- `@theme` in CSS defines tokens.
- No `tailwind.config.js` by default.
- Tokens are CSS custom properties, accessible everywhere.
- Faster compilation, simpler mental model.

Migrating v3 → v4 is non-trivial; check the official migration guide. New projects in late 2025 onwards should default to v4.

## Token configuration (v4)

```css
@theme {
  --color-bg: oklch(98% 0 0);
  --color-fg: oklch(15% 0 0);
  --color-accent: oklch(60% 0.2 25);
  --color-muted: oklch(50% 0 0);
  --color-border: oklch(90% 0 0);

  --font-sans: 'Inter', system-ui, sans-serif;
  --font-serif: 'Fraunces', Georgia, serif;
  --font-mono: 'JetBrains Mono', monospace;

  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
}
```

These become `bg-bg`, `text-fg`, `text-accent`, `font-sans`, `rounded-md`, etc.

## Token configuration (v3)

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        bg: '#FAFAFA',
        fg: '#0F172A',
        accent: '#FF6A1F',
        muted: '#64748B',
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        serif: ['Fraunces', 'Georgia', 'serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
    },
  },
};
```

`extend` adds to the defaults; replacing the whole `colors` object (without `extend`) removes the default palette entirely. For semantic-only tokens, replace; to keep `red-500` etc available, extend.

## Class ordering

Tailwind class strings get long. Use a consistent order:

1. Layout (`flex`, `grid`, `block`, `hidden`)
2. Position (`absolute`, `relative`, `inset-0`)
3. Box (`w-`, `h-`, `m-`, `p-`)
4. Typography (`text-`, `font-`, `leading-`)
5. Colour and background (`bg-`, `text-fg`, `border-`)
6. Effects (`shadow-`, `opacity-`, `blur-`)
7. Interaction states (`hover:`, `focus:`, `disabled:`)
8. Responsive prefixes (`sm:`, `md:`, `lg:`)

Use `prettier-plugin-tailwindcss` to enforce ordering automatically.

## Avoiding class soup

When a className gets longer than ~80 characters or has more than a dozen utilities, extract.

**Options for extraction:**

1. **Component**: `<Button>` wraps the utilities, props expose variants.
2. **`class-variance-authority` (cva)** or **`tailwind-variants` (tv)**: a structured way to define variants in a single source.
3. **`@apply` in CSS**: for genuinely cross-cutting styles (`.prose`, `.card-base`). Don't use for one-off components.

Example with cva:

```ts
import { cva } from 'class-variance-authority';

export const button = cva(
  'inline-flex items-center justify-center font-medium transition-colors focus-visible:outline-none focus-visible:ring-2',
  {
    variants: {
      variant: {
        primary: 'bg-accent text-white hover:bg-accent/90',
        secondary: 'bg-muted text-fg hover:bg-muted/80',
        ghost: 'text-fg hover:bg-muted/20',
      },
      size: {
        sm: 'h-8 px-3 text-sm',
        md: 'h-10 px-4 text-base',
        lg: 'h-12 px-6 text-lg',
      },
    },
    defaultVariants: { variant: 'primary', size: 'md' },
  }
);
```

## Responsive and state prefixes

- **Mobile-first.** Base classes are mobile; `sm:`, `md:`, `lg:`, `xl:`, `2xl:` add on for larger screens.
- **State stacking**: `hover:`, `focus:`, `focus-visible:`, `active:`, `disabled:`, `group-hover:`, `peer-checked:`. Each addresses a specific scenario.
- **`focus-visible` over `focus`** for keyboard-only focus rings. `focus` triggers on click too, which is usually noisy.

## Dark mode

```css
/* v4 */
@variant dark (&:where(.dark, .dark *));
```

```js
// v3
module.exports = {
  darkMode: 'class', // or 'media' for system-driven
};
```

Then use `dark:` prefix: `bg-white dark:bg-zinc-900 text-zinc-900 dark:text-zinc-100`.

**For tokenised colour systems**, prefer redefining tokens in dark mode rather than peppering `dark:` everywhere:

```css
@theme {
  --color-bg: oklch(98% 0 0);
  --color-fg: oklch(15% 0 0);
}
.dark {
  --color-bg: oklch(12% 0 0);
  --color-fg: oklch(95% 0 0);
}
```

Then `bg-bg text-fg` works in both modes without `dark:` prefixes.

## Plugins

Tailwind plugins extend the framework. Useful ones:

- **`@tailwindcss/typography`** — `prose` classes for long-form content.
- **`@tailwindcss/forms`** — sane form input defaults.
- **`@tailwindcss/aspect-ratio`** — built-in in modern Tailwind, no plugin needed.
- **`tailwindcss-animate`** — animation utilities used by shadcn/ui.

Avoid plugin bloat. Each plugin adds compilation cost and surface area.

## Common anti-patterns

- **Hard-coded hex values** (`text-[#3B82F6]`). Use a token.
- **Inconsistent spacing** (`p-3` here, `p-3.5` there, `p-[14px]` elsewhere). Pick one scale and stay on it.
- **Inline `style={{}}`** for things Tailwind could do. The escape hatch is for values genuinely outside the system.
- **Using `!important` (`!`) prefix.** Specificity wars are a tell that the cascade isn't being respected.
- **Mixing utility approaches.** Tailwind + emotion + styled-components in the same project is a mess. Pick one.

## When to leave Tailwind

Some patterns are uncomfortable in utility CSS:

- **Complex animation keyframes**: define in `@keyframes`, reference via Tailwind.
- **Pseudo-element decoration** (`::before` with content): plain CSS in a module or `<style>` block.
- **Generated content patterns** (counters, gradients with specific math): plain CSS.

Tailwind is a tool. Use it for 90% of the work and reach for plain CSS for the 10% that fights it.

## Performance

- **Production builds purge unused classes** automatically. Tree-shaking is free.
- **Avoid dynamic class names** (`className={`bg-${color}-500`}`). The Tailwind compiler can't see them; they get purged. Use safelisting or precomputed class maps.
- **Critical CSS**: in SSR contexts, inline the above-the-fold CSS for faster first paint.

## With shadcn/ui

shadcn/ui is the dominant component recipe layered on Tailwind. Use it as a starting point, not a final state:

- **Reskin tokens through your design system** before composing pages. Default shadcn looks like every other shadcn site.
- **Modify the components.** They're copied into your repo, not consumed from a package. Edit freely.
- **Don't reach for every shadcn component.** Use the ones that fit; build the ones that don't.

## What to verify before declaring Tailwind work done

- Are tokens defined, with no arbitrary values in production code?
- Are class strings under ~80 characters, or extracted to components?
- Is class order consistent (use the prettier plugin)?
- Is dark mode handled via tokens, not `dark:` proliferation?
- Have you removed unused plugins from the config?
- Does the build size pass your budget after purge?
