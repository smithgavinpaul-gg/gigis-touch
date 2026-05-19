# Texture & Material

Synthesised from the texture/visual-resource skills (`claudedesignskills`, `jezweb/claude-skills`, Anthropic's `algorithmic-art`, `canvas-design`, `brand-guidelines`).

Texture is what stops a screen from looking like a wireframe. A surface without material reads as a placeholder; a surface with the right material reads as a place.

## Core positions

1. **A texture must have a reason.** Grain because the surface should feel printed. Halftone because the surface references image reproduction. Paper because the content should feel read. Without a reason, texture is decoration.
2. **Texture is a system property, not a sticker.** Apply it consistently across the product, or not at all. Inconsistent texture (one page grainy, the next clean) reads as forgotten.
3. **Less than you think.** Grain at 6% feels intentional; grain at 25% feels broken. Halftone at small dot size looks photographic; at large dot size looks like a meme. Calibrate down.
4. **Texture must not fight legibility.** Whatever the texture, body type must remain crisp against it. Test by reading a paragraph for 30 seconds; if your eyes drift, the texture is too loud.
5. **Materials replace skeuomorphism.** Modern texture is not "this looks like leather" or "this looks like glass". It is "this surface has weight, history, or print-ness". The reference is real-world media, not real-world objects.

## Common textures and their meanings

- **Grain / noise** — printed, photographic, considered. Suits editorial, brutalist, and editorial-leaning product work. Use at 4-8% opacity over solid backgrounds, monochrome noise (slightly warm for paper feel, slightly cool for engineered feel).
- **Paper texture** — read, contemplative. Suits long-form, manuscript, editorial work. Often a subtle bone background hue + low-opacity noise + slightly warm shadows.
- **Halftone** — graphic, retro, print-reproduction. Suits posters, brand-led work, comic-adjacent design. Used cleanly, not as a "vintage" stamp.
- **Gradients (mesh)** — atmospheric, premium when restrained. Suits dashboards, marketing, brand. Use at low saturation and large soft blobs.
- **Film grain in video** — cinematic, slowed-down. Suits Remotion pieces, hero videos, motion graphics. Apply as the final pass.
- **Glass / frosted blur** — modern but dating. Suits OS-level interfaces (overlays, command palettes), avoid as primary product texture.
- **Brutalist concrete / scan-line** — strong stylistic choice. Suits a specific design language; not a general-purpose texture.

## Grain implementation

CSS approach (cheap, no asset):

```css
.grain {
  position: relative;
}
.grain::after {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' /%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.5'/%3E%3C/svg%3E");
  opacity: 0.06;
  mix-blend-mode: overlay;
}
```

Tune `baseFrequency` for grain size (higher = finer grain) and `opacity` for intensity. For warm grain, increase the SVG noise's red channel slightly via a feColorMatrix.

## Halftone

- Best generated via SVG patterns or canvas, not raster images, so they scale.
- Dot spacing should relate to the type scale — coarser for display, finer for body backgrounds.
- Two colours work best (one ground, one dot). Adding more breaks the print-reproduction reference.

## Paper

Paper is grain + warm hue + sometimes a subtle vignetting at the edges. The bone-warm background does most of the work; grain finishes it.

```css
:root {
  --paper-bg: #F1ECE2;
  --paper-ink: #1A1714;
}
body {
  background: var(--paper-bg);
  color: var(--paper-ink);
}
```

Add a low-opacity grain overlay and the page feels printed without being literal.

## Light, shadow, depth

Three eras of digital "depth":

1. **Skeuomorphism** (pre-2013) — literal real-world materials. Mostly dated; surfaces of return.
2. **Flat** (2013-2020) — no depth at all. Easy, often boring.
3. **Soft, considered depth** (2020-) — subtle shadows that suggest a slight elevation rather than mimicking a real surface.

Modern shadow discipline:

- **Layered shadows.** A single `box-shadow: 0 4px 12px rgba(0,0,0,0.1)` reads cheap. Two stacked shadows (one tight, one diffuse) read refined: `box-shadow: 0 1px 2px rgba(0,0,0,0.04), 0 8px 16px rgba(0,0,0,0.06)`.
- **Coloured shadows.** Tinted to the element's colour, slightly darker, slightly more saturated. A red button casts a faint red shadow, not a pure grey one.
- **Shadow elevation system.** Define 4-5 elevation levels (none, hairline, low, medium, high) with paired shadow values. Use them consistently.

In dark mode, surfaces elevate by *getting lighter*, not by casting darker shadows. A hover-card 6% lighter than the canvas reads as raised.

## Imagery treatment

When real photographs sit in a designed surface, they often clash because they bring their own colour, light, and contrast. Treatments:

- **Desaturate** to 60-80% so colours integrate with the palette.
- **Match foreground temperature.** If the design is warm, warm the photo's highlights and shadows slightly.
- **Apply matching grain overlay** so the photo sits in the same material world as the surface.
- **Crop tighter, use larger.** A photo that fills its container feels designed; a photo floating in a polaroid frame feels stock.
- **Black-and-white** is always an option. Removes the colour clash entirely.

## Icons and illustration

- Icons and illustrations carry texture choices too: a fine-line illustration on a grainy editorial page; a flat solid illustration on a clinical product page.
- Match line weight to the type weight. A 1px illustration paired with 700-weight type looks underweight; a 3px illustration paired with 400-weight type looks heavy.
- Custom illustration > stock illustration, every time.

## Combining textures

If you use texture, commit to one *primary* material per product. Mixing grain + glass + gradients + halftone is incoherent. Pick a primary, allow at most one secondary in specific contexts (e.g. grain everywhere, with subtle gradient meshes on the marketing hero only).

## Performance

- SVG noise and CSS gradients render essentially free.
- PNG noise overlays should be tiny (32×32 to 200×200) and tiled, not full-screen images.
- Mesh gradients via CSS (`background: radial-gradient(... at X% Y%), radial-gradient(...)`) are cheap; via raster images are heavy and unscalable.
- Glass blur (`backdrop-filter`) is GPU-expensive; use sparingly and never on scrolling regions.

## What to verify before declaring texture done

- Does the texture have a reason traceable to the product's content?
- Is the texture consistent across the product, or have you forgotten pages?
- Have you calibrated grain opacity down to 4-8%?
- Does body text remain crisp against the textured surface?
- Are shadows layered (two stacked) rather than single?
- In dark mode, does elevation rely on lighter surfaces rather than darker shadows?
- Have you avoided combining three or more texture systems?
