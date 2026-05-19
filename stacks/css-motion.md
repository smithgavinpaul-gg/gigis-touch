# CSS Motion

Synthesised from the CSS animation skill (`neonwatty/css-animation-skill`) and the motion sections of the foundational frontend skills.

CSS handles 90% of the motion needs in modern interfaces. The principles in `principles/motion.md` apply; this file translates them to the CSS surface.

## Core positions

1. **Use CSS for transitions and short animations; reach for JS only when needed.** CSS is more performant, more declarative, and degrades better.
2. **Transitions are for state changes; animations are for sequences.** A button-hover is a transition. A loading dot loop is an animation.
3. **Animate transform and opacity.** These are GPU-accelerated and don't trigger layout/paint. Animating `width`, `height`, `top`, `left` causes jank.
4. **Honour `prefers-reduced-motion` at the system level**, not per-component.
5. **`will-change` is a promise, not a free GPU pass.** Apply only to elements actively animating, remove after.

## Transitions

For state-driven motion (hover, focus, active, classname toggle):

```css
.button {
  background: var(--accent);
  transition: background 200ms cubic-bezier(0.4, 0, 0.2, 1),
              transform 100ms cubic-bezier(0.4, 0, 0.2, 1);
}
.button:hover {
  background: color-mix(in oklch, var(--accent), white 10%);
}
.button:active {
  transform: scale(0.98);
}
```

- **Transition only the properties that change.** `transition: all` is lazy and animates unintended properties.
- **Pair properties with durations and easings.** Hover backgrounds want 150-200ms; transforms want 100-150ms (faster, snappier).
- **Use `cubic-bezier` over `ease`.** Browser defaults are too symmetric for most cases.

## Keyframe animations

For looping or scripted sequences:

```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(8px); }
  to   { opacity: 1; transform: translateY(0); }
}

.reveal {
  animation: fadeUp 400ms cubic-bezier(0.16, 1, 0.3, 1) both;
}
```

- **`both`** keeps the starting and ending states applied before and after the animation runs.
- **`forwards`** keeps only the end state. Use when the element should retain its final position.
- **`infinite`** for loops. Always pair with a sensible duration or you'll have a strobe.

## Staggered entries

For lists or grids entering one after another:

```css
.list-item {
  opacity: 0;
  animation: fadeUp 400ms cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
.list-item:nth-child(1) { animation-delay: 50ms; }
.list-item:nth-child(2) { animation-delay: 100ms; }
.list-item:nth-child(3) { animation-delay: 150ms; }
/* ... */
```

Or with a CSS custom property + inline style:

```css
.list-item {
  opacity: 0;
  animation: fadeUp 400ms cubic-bezier(0.16, 1, 0.3, 1) forwards;
  animation-delay: calc(var(--i) * 50ms);
}
```

```html
<li class="list-item" style="--i: 0;">...</li>
<li class="list-item" style="--i: 1;">...</li>
```

## Reduced motion

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

This is a baseline. Better: define non-motion alternatives (a simple show/hide instead of a slide-in) for users who request reduced motion, while keeping the *informational* content of the motion (the element appears, just without travel).

## `transform` discipline

Use `transform: translate(x, y)`, `scale()`, `rotate()`, `skew()`. These compose:

```css
transform: translate(0, 8px) scale(1.02) rotate(2deg);
```

Order matters: `translate(...) scale(...)` and `scale(...) translate(...)` produce different results. For most UI work, translate before scale before rotate is a stable pattern.

## `will-change`

```css
.modal {
  will-change: transform, opacity;
}
```

- Apply *just before* the animation starts (e.g. when the modal mounts).
- Remove after the animation completes.
- Don't apply globally. Permanent `will-change` on many elements is worse than none.

## Scroll-linked animation

Modern CSS supports scroll-driven animations:

```css
@keyframes appear {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

.section {
  animation: appear linear;
  animation-timeline: view();
  animation-range: entry 0% cover 30%;
}
```

This drives the animation by scroll position rather than time. No JavaScript required. Check current browser support; fall back to IntersectionObserver where needed.

## View transitions

The View Transitions API (`document.startViewTransition()`) animates between DOM states automatically:

```js
function navigate(href) {
  if (!document.startViewTransition) {
    window.location.href = href;
    return;
  }
  document.startViewTransition(() => {
    // perform the DOM update (e.g., fetch + replace content)
  });
}
```

Browsers handle the crossfade by default; customise via `::view-transition-*` pseudo-elements.

## Common patterns

**Fade in from below:**

```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(8px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

**Slide in from right:**

```css
@keyframes slideIn {
  from { transform: translateX(100%); }
  to   { transform: translateX(0); }
}
```

**Scale and fade (modal entry):**

```css
@keyframes modalIn {
  from { opacity: 0; transform: scale(0.96); }
  to   { opacity: 1; transform: scale(1); }
}
```

**Skeleton shimmer:**

```css
@keyframes shimmer {
  to { background-position-x: -200%; }
}

.skeleton {
  background: linear-gradient(90deg, #eee 0%, #ddd 50%, #eee 100%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite linear;
}
```

**Bouncing dot (loading):**

```css
@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50%      { transform: translateY(-4px); }
}

.dot {
  animation: bounce 600ms infinite ease-in-out;
}
.dot:nth-child(2) { animation-delay: 100ms; }
.dot:nth-child(3) { animation-delay: 200ms; }
```

## Spring physics in CSS

Native CSS doesn't ship springs, but `linear()` easing (modern browsers) approximates them:

```css
.bouncy {
  transition: transform 400ms linear(
    0, 0.13, 0.5, 0.85, 1.05, 1.08, 1.05, 1.02, 1
  );
}
```

For richer spring control, use a JS animation library (Framer Motion, Motion One, GSAP).

## Performance debugging

- **Chrome DevTools > Performance**: record an animation, check for "long frames" (>16ms).
- **Layers panel** (Rendering tab): shows which elements are on their own compositor layer.
- **Animations panel**: scrub through animations at 4× slow-down.
- **Common cause of jank**: animating `width`/`height`/`top`/`left`, or animating an element with many children.

## What to verify before declaring CSS motion done

- Are you animating transform and opacity, not layout properties?
- Is `prefers-reduced-motion` respected?
- Are durations role-appropriate (instant for hover, deliberate for entry)?
- Are easings role-appropriate (ease-out for entry, ease-in for exit)?
- Is `will-change` applied only when needed, removed after?
- At 4× slow-down, does the motion still feel right?
- Have you eliminated any decorative loops that don't serve a purpose?
