# Accessibility

Synthesised from the a11y discipline in the foundational design skills and the UX-focused repos.

Accessibility is not a separate concern after design; it is one of the constraints that *makes* a design good. Inaccessible work is unfinished work.

## Core positions

1. **Inclusive by default.** Design for the widest range of users, then refine. Treating accessibility as an afterthought produces retrofitted compromises.
2. **Semantics first, ARIA second.** A correctly structured HTML page is 80% accessible without effort. ARIA fixes specific edge cases; it does not rescue bad markup.
3. **Disability is contextual.** A user with full vision in a sunlit street has low-vision needs. A user with full hearing on a quiet train has captioning needs. Accessibility serves everyone, sometimes.
4. **Keyboard is the universal input.** A user navigating by keyboard (screen reader, motor disability, power user) should be able to complete every task. If they can't, the product is broken.
5. **WCAG AA is the legal floor, not the goal.** Aim higher; AAA where reading is the task.

## The WCAG four pillars

WCAG organises requirements under POUR:

- **Perceivable** — users can sense the content (visually, audibly, or assistively).
- **Operable** — users can interact (mouse, touch, keyboard, voice).
- **Understandable** — content reads clearly, behaviour is predictable.
- **Robust** — works across browsers, devices, assistive technologies.

Use POUR as a self-review structure.

## Colour and contrast

(See `principles/color.md` for full discussion.) Quick rules:

- Body text against background: 4.5:1 minimum (AA), aim 7:1 (AAA) where reading is the task.
- Large text (18pt+ or 14pt+ bold): 3:1 minimum.
- UI components (button borders, focus rings, icons that convey meaning): 3:1 against adjacent colours.
- **Never rely on colour alone.** Errors need shape/icon/text, not just red. Selected states need outline or fill change, not just colour shift.
- Test in a colour-blindness simulator (Chrome DevTools > Rendering > Emulate vision deficiencies).

## Type and reading

- Minimum body size: 16px on web, larger if the audience skews older.
- Line-length 45-75 characters for prose.
- Sufficient line-height (1.5+ for body).
- Avoid full-justified text; jagged right edges read more naturally for most users (and especially dyslexic readers).
- Avoid all-caps for body prose; the lack of ascender/descender variation slows reading.

## Keyboard navigation

- **Every interactive element reachable by Tab.** Custom controls (div-as-button) must implement focus + keyboard handlers.
- **Visible focus indicator.** Never `outline: none` without a replacement. The focus ring should be ≥2px and 3:1 contrast against its background.
- **Logical tab order.** Should match visual reading order. Use `tabindex="0"` to make non-interactive elements focusable when needed; avoid positive `tabindex` values (they break order).
- **Escape closes overlays.** Modals, popovers, command palettes all close on Esc.
- **Enter / Space activate.** Both for buttons. Enter alone for links.
- **Skip links** at the top of long pages: "Skip to content". Visible on focus.

## Screen readers

- **Use real HTML elements.** `<button>` for buttons, `<a href>` for links, `<input>` for inputs, `<nav>`, `<main>`, `<aside>`, `<header>`, `<footer>` for landmarks.
- **Heading hierarchy** is the screen reader's table of contents. One `<h1>`, descending levels without skipping.
- **Alt text for images.** Descriptive for content images, `alt=""` for decorative ones. Not "image of...".
- **ARIA labels for icon-only buttons.** A close button with just an X icon needs `aria-label="Close"`.
- **Live regions** for dynamic content. Toasts, in-progress updates, errors should announce via `aria-live="polite"` (most) or `aria-live="assertive"` (urgent).
- **Hidden visually but not from screen readers**: use `.sr-only` (a class that visually hides content but keeps it in the accessibility tree).

## Motion and animation

- **Honour `prefers-reduced-motion`.** Reduce animations to crossfades or remove them entirely. See `principles/motion.md`.
- **No flashing content >3 times per second.** This is a seizure-risk threshold.
- **Auto-play video should have controls and be muted.** Better: don't autoplay.

## Touch targets

- **44×44px minimum** (iOS HIG) / 48×48dp minimum (Android Material).
- **Spacing between targets** at least 8px so users don't tap the wrong one.
- **Forgiving hit areas**: a 24px icon button can have a 44px tappable region via padding.

## Forms

- **Labels are persistent** above (or beside) every input. Placeholders are not labels; they vanish.
- **Required fields marked** with asterisk + "required" text, not just colour.
- **Error messages associated** via `aria-describedby` so screen readers announce them.
- **Autocomplete attributes** (`autocomplete="email"`, `autocomplete="given-name"`) help password managers and screen readers.
- **Input modes** for mobile keyboards (`inputmode="numeric"`, `inputmode="email"`).

## Language and reading level

- **Set the page language**: `<html lang="en">`. Set inline language changes too: `<span lang="fr">`.
- **Plain language**. Avoid jargon where possible. Define jargon on first use.
- **Reading age 13-15** for general audiences. Tools like Hemingway and readable.io flag complex sentences.
- **No idioms in critical UI text.** "Kick the tyres" is invisible to non-native speakers.

## Time and interaction

- **Don't impose tight time limits.** Session timeouts, captcha countdowns, "you have 30 seconds" patterns punish users with motor or cognitive disabilities. If timeouts are necessary (security), allow extension.
- **Don't auto-advance content** (carousels, slideshows) unless pausable. Auto-advance steals focus from users who read slowly.

## Beyond WCAG

WCAG is a baseline. Beyond it:

- **Cognitive load reduction.** See `principles/ux.md`. Group, chunk, hide complexity, surface recognition.
- **Anxiety reduction.** Show progress through long flows. Make undoing easy. Avoid surprise confirmations.
- **Language**. Plain words for emotionally heavy moments (errors, account deletion, payment failure).

## Tools and checks

- **axe DevTools** (browser extension) — automated WCAG check, catches ~30% of issues. Run on every page.
- **WAVE** (browser extension) — visualises accessibility issues directly on the page.
- **Lighthouse accessibility audit** — built into Chrome DevTools.
- **VoiceOver (Mac), NVDA (Windows), TalkBack (Android)** — actually test with a screen reader. Automated tools miss meaningful failures.
- **Keyboard-only navigation test**: unplug your mouse, complete a primary flow. If you can't, fix it.

## What to verify before declaring accessibility done

- Have you tabbed through the page in order?
- Is the focus ring visible everywhere?
- Have you run axe DevTools or Lighthouse with no critical issues?
- Have you tested at least one flow with VoiceOver or NVDA?
- Does colour pass contrast at AA minimum, AAA for body where possible?
- Are all images either described or marked decorative?
- Are all icon-only buttons labelled?
- Is the page navigable at 200% zoom without horizontal scroll?
- Does the page work with `prefers-reduced-motion: reduce`?
- Are touch targets at least 44×44px on touch devices?
