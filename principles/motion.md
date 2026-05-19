# Motion

Synthesised from the motion-oriented skills (`motion-dev-animations-skill`, `wiggle-claude-skill`, `css-animation-skill`) and the motion sections of the foundational design skills.

Motion is communication, not decoration. Every animation should answer a question the user has implicitly asked: where did that come from, what just happened, where is it going, can I act now.

## Core positions

1. **Motion explains causality.** When something appears, moves, or transforms, motion can show *why*. A modal that scales up from a button tells the user the button caused it. A list item that slides into place tells the user *where it came from*.
2. **Stillness is the baseline.** Motion is the exception, not the default. A page that moves constantly fatigues the user; a still page that moves at meaningful moments feels alive.
3. **Easing is character.** Linear motion is mechanical, ease-in-out is polite, ease-out is decisive, springs are playful, bounces are juvenile. Pick the character on purpose.
4. **Duration is rhythm.** 100ms feels instant, 200-300ms feels responsive, 400-600ms feels considered, 800ms+ feels deliberate or slow. Match the duration to the role of the motion.
5. **Respect reduced motion.** `prefers-reduced-motion` is not optional. Vestibular conditions exist; an animation you can't see has zero benefit and meaningful harm.

## When to animate

- **Entry and exit of meaningful surfaces.** Modals, sheets, drawers, toasts, tooltips.
- **State transitions.** A toggle flipping, a tab content changing, a list item being removed.
- **Acknowledgement of an action.** A button confirming a click, a heart filling on like.
- **Guiding attention.** A new item entering a list, a counter incrementing, a notification arriving.
- **Spatial continuity.** When one element transforms into another (an item card expanding into a detail page), motion preserves the user's sense of place.

## When *not* to animate

- Every paragraph fading in on scroll. Reading should not be a performance.
- Hover effects that distort layout (scale 1.05 on cards). They cause jumpy cursor tracking.
- Decorative wiggle, jitter, or constant looping behind static content.
- Page transitions on every navigation. A 400ms crossfade between every route doubles every navigation time. Use transitions selectively.
- Loading spinners that take longer than the actual load. If the work is fast, just show the result.

## Duration ranges

| Role | Duration | Notes |
|---|---|---|
| Hover / focus | 100-150ms | Should feel instant but not invisible |
| State change in place (toggle, tab) | 150-250ms | Snappy |
| Element entry / exit | 200-400ms | Long enough to track |
| Page or section transition | 300-500ms | Tells the user this is a context shift |
| Hero or cinematic reveal | 600-1200ms | Deliberate; usually once per page |
| Choreographed sequence | up to 1500ms total | Multiple staggered elements |

If a single animation exceeds 600ms without a hero purpose, it is too slow.

## Easing curves

The named curves and their characters:

- **`linear`** — mechanical, conveyor-belt. Use for indefinite progress, never for UI transitions.
- **`ease-out`** (`cubic-bezier(0, 0, 0.2, 1)`) — decisive arrival. The element shoots in and settles. **The default for entering motion.**
- **`ease-in`** (`cubic-bezier(0.4, 0, 1, 1)`) — gradual departure. The element accelerates as it leaves. **The default for exiting motion.**
- **`ease-in-out`** (`cubic-bezier(0.4, 0, 0.2, 1)`) — smooth both ends. For state changes that don't have a clear direction.
- **`cubic-bezier(0.16, 1, 0.3, 1)`** — soft spring-like ease-out. Premium feel.
- **`cubic-bezier(0.85, 0, 0.15, 1)`** — sharp ease-in-out. Editorial, deliberate.
- **`cubic-bezier(0.34, 1.56, 0.64, 1)`** — overshoot. Playful entrance, occasional use only.
- **Spring physics** (Framer Motion, React Spring, CSS Houdini) — natural-feeling, parameterised by stiffness, damping, mass. Replaces durations.

## The most-broken default

Most "designed" sites use `ease-in-out` everywhere or, worse, the browser's default `ease`. Replace with role-appropriate curves:

- Entry: `ease-out` or `cubic-bezier(0.16, 1, 0.3, 1)`.
- Exit: `ease-in` or `cubic-bezier(0.4, 0, 1, 1)`.
- State change: `ease-in-out`, but consider whether the change has direction.

## Spring physics

Springs replace duration + easing with stiffness + damping + mass. They feel more natural because real objects move on springs, not curves.

- **Stiffness**: how tight the spring is. Higher = faster, snappier.
- **Damping**: how much friction. Higher = less bouncy, more controlled.
- **Mass**: how heavy the element is. Higher = slower acceleration.

Starting points:

- UI default: stiffness 300, damping 30, mass 1.
- Playful: stiffness 400, damping 20, mass 1 (more bounce).
- Refined: stiffness 200, damping 40, mass 1 (no overshoot).

## Choreography

When multiple elements animate together:

- **Stagger entry.** Items enter one after another, usually 30-80ms apart. The eye can follow individual entries, then the group as a whole.
- **Lead with the largest element.** Or the most important. Smaller elements settle in around it.
- **Exit is faster than entry.** Things leave more quickly than they arrived; the user is moving on.
- **One element holds focus at a time.** Don't ask the eye to track three independent animations simultaneously.

## Scroll-linked motion

- **Subtle parallax** on hero imagery can work; aggressive parallax disorients.
- **Reveal-on-scroll** for sections, not for every paragraph. Use a generous threshold (element 25% into viewport) so reveals feel deliberate.
- **Sticky elements** (sticky headers, sticky CTAs) are motion through context, not motion through transform. Treat their entry/exit (sticky → not sticky) as a state change worth animating.
- **Avoid scroll-jacking** unless the entire experience is a story-driven scroll (rare and difficult to do well).

## Micro-interactions

The small motions that signal a system is alive:

- A button that gently scales (0.97-0.98) on press.
- A toggle whose thumb springs into place.
- A heart that pops slightly when liked.
- A focus ring that animates in when an input is focused.
- A text input whose label transitions from placeholder to floating label.

These should be < 200ms, with a clear cause (user input) and a clear acknowledgement. They make products feel responsive.

## Performance

- **Animate transform and opacity only**, except where genuinely needed otherwise. These are GPU-accelerated and don't trigger layout.
- Avoid animating `width`, `height`, `top`, `left`, `margin`, or anything that triggers layout. Use `transform: translate / scale` instead.
- **`will-change` is a hint, not a command.** Apply it to elements about to animate, remove it after. Permanent `will-change` on many elements pessimises performance.
- **60fps is the target.** If a motion stutters, profile it. A janky animation is worse than no animation.

## Reduced motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

This is a baseline. Better: replace motion with crossfade or no transition for users who request reduced motion, while keeping the *information* the motion conveyed.

## What to verify before declaring motion done

- Does every animation answer a "why is this moving?"
- Are durations matched to roles (instant for hover, deliberate for entry, long for hero)?
- Are easing curves role-appropriate (ease-out for entry, ease-in for exit)?
- Is `prefers-reduced-motion` respected?
- Are you animating transform and opacity, not layout properties?
- Have you tested the motion at 4x slow-down? (DevTools > Animations panel.)
- Have you removed any decorative motion that wasn't earning its place?
