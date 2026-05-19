# Colour

Synthesised from the foundational design skills, the brand-guidelines skill in Anthropic's official set, and the colour discipline across UI/UX repos.

Colour is the fastest carrier of meaning on a screen. Wielded with restraint it organises and dignifies; wielded loosely it shouts.

## Core positions

1. **Limit the palette before you expand it.** Five hues is generous. Three is often enough. Most "designed" interfaces use two hues plus a neutral ramp.
2. **Decisions should map to roles, not aesthetics.** Define what each colour *means* in the system (foreground, surface, accent, success, danger), then pick the swatches. Do not pick swatches first and find roles for them.
3. **Contrast is more important than colour.** A dull product with strong contrast is legible; a vibrant product with weak contrast is not. WCAG AA is a floor, not a goal.
4. **Neutrals carry most of the work.** 80%+ of pixels in any well-designed product are some shade of neutral. The accent is the spice, not the meal.
5. **Light and dark are different products.** Dark mode is not a CSS variable flip; it is a parallel palette that needs its own discipline. Re-derive contrast, re-balance accent saturation, re-test imagery.

## Token roles

A minimum role-based palette:

| Role | Purpose | Typical count |
|---|---|---|
| Foreground | Body text, primary icons | 1 primary + 2-3 graded |
| Background | Page canvas | 1 primary + 1-2 elevated surfaces |
| Surface | Cards, panels, sheets | 1-2 |
| Border | Hairlines, dividers | 1-2 |
| Muted | Metadata, placeholder text | 1-2 |
| Accent | Primary brand colour | 1 |
| Accent-hover / pressed | Interactive feedback | derived from accent |
| Success | Positive state | 1 |
| Warning | Caution state | 1 |
| Danger | Destructive / error state | 1 |
| Info | Informational state | 1 (optional) |

Implement as design tokens (CSS custom properties, Tailwind theme tokens, design system variables) so a single source of truth drives every usage.

## Neutral ramps

A working neutral ramp has 10-12 steps from white to black. Tailwind's `slate`, `zinc`, `neutral`, `gray`, and `stone` are reasonable starting points; the difference is hue temperature:

- **Slate, zinc**: cool grey, engineered feel.
- **Neutral, gray**: true grey, neutral character.
- **Stone**: warm grey, paper-feel, suits editorial.

Pick one temperature and commit. Mixing warm and cool neutrals in the same product reads as accidental.

## Accent discipline

- **One primary accent.** A second accent is allowed only when it serves a structural purpose (e.g. a category tag system with distinct categories). Two accents for "visual interest" is decoration.
- **Saturation is a dial.** Pastels feel friendly and editorial, fully saturated accents feel commercial and energetic, desaturated accents feel premium and considered. Choose deliberately.
- **The accent should pass contrast against the page background at the size it is used.** A 16px body link in your accent needs 4.5:1 against the page; a 32px headline needs 3:1.

## Gradients

Gradients are a strong choice when intentional, a tell when default. Rules:

- **Two-stop gradients only**, in most cases. Three stops start to look like a marketing template.
- **Stay in adjacent hues**, not across the wheel. A blue-to-violet gradient is cohesive; a green-to-pink gradient is loud.
- **Use them for surface, not text.** Gradient text is a tell except in genuinely playful contexts.
- **Mesh gradients** (radial blobs blended) read as premium when controlled, AI-generic when default. Limit to one per page, large, soft, behind content.

## Dark mode

- **Do not invert.** A literal colour-inversion of a light mode is unbalanced. Re-derive the palette.
- **Reduce saturation in dark mode.** Colours read more saturated against dark backgrounds; a vibrant blue that works on white may need to be dialled back on near-black.
- **Avoid pure black backgrounds.** Pure #000 produces halation around bright text on OLED displays and feels harsh. Use #0A0A0A, #0E0E10, #111, or a dark slate as your true "black".
- **Avoid pure white foregrounds.** Slight off-white (#F4F4F5, #FAFAF9) reduces eye strain on dark backgrounds at high brightness.
- **Surface elevation in dark mode** is shown by *lighter* surfaces, not darker shadows. Elevated cards on a near-black canvas are 4-8% lighter.

## Light mode

- **Off-white canvases** (e.g. #FAFAFA, #F5F5F4, #F1ECE2) often read better than pure white, especially for long-form reading.
- **Pure white for clinical, editorial, or product photography contexts** where the white serves as a stage.
- **Foreground rarely needs to be pure black.** Slight warm or cool dark (#0F172A, #18181B, #1A1714) carries more refinement and is easier on the eye at body size.

## Semantic colours

- **Success**: usually green, but a desaturated, slightly bluish green (forest, teal-leaning) reads more refined than a fluorescent green.
- **Warning**: amber or honey, not pure yellow (which is hard to read at small sizes).
- **Danger**: red, but pulled slightly towards crimson or coral if the brand is warm, or towards true red if the brand is engineered.
- **Info**: blue, but not the same blue as your accent if your accent is also blue. Pick a sibling.

Always pair semantic colour with shape or icon. A red border alone is not enough for colourblind users; a red border + an error icon + a clear message is.

## Colour blindness

- 8% of men and 0.5% of women have some form of colour vision deficiency. Most commonly red-green.
- **Never rely on red vs green alone.** A red bar and a green bar must also differ by shape, position, or label.
- Test palettes with a colour-blindness simulator (Chrome DevTools has one built in).

## Contrast

- **WCAG AA**: 4.5:1 for normal text, 3:1 for large text (18pt+ or 14pt+ bold).
- **WCAG AAA**: 7:1 for normal, 4.5:1 for large. Aim for AAA in long-form reading surfaces and tools.
- Body foreground against page background: AAA where possible.
- Placeholder text and metadata: AA minimum, do not slip below.
- Interactive elements (buttons, links, focus rings): AA against their background.

## Brand colour as a single source of truth

The brand colour should appear in:

- Primary CTA fill.
- Active states in navigation.
- Selection highlights (text selection, table row selection).
- Focus rings, if the brand colour passes contrast.
- Loading bars and progress indicators.
- Brand mark (logo).

It should *not* appear in:

- Body text foreground (except for links).
- Every heading.
- Background panels (unless very desaturated).
- All buttons (only the primary).

## What to verify before declaring colour done

- Is the palette implemented as tokens with semantic roles?
- Is the accent count one (with rare structural exceptions)?
- Does body foreground hit AAA against the page background?
- Are interactive elements at AA against their context?
- Is dark mode re-derived, not inverted?
- Have you tested the page in a colour-blindness simulator?
- Does the canvas avoid pure #000 and #FFF where it should?
- Are gradients (if any) two-stop and in adjacent hues?
