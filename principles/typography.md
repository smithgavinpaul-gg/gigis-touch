# Typography

Synthesised from the typography skills (`open-design`, `glebis/claude-skills`) and the typographic discipline embedded in the foundational frontend-design skills.

Typography is the largest, most-seen surface in almost every digital product. Most "redesigns" are 80% typography fixes; treat it as load-bearing.

## Core positions

1. **Pick a type system, not a font.** A system is: one display face (optional), one body face, and optionally one mono. The relationship between them is the work; the individual choices are secondary.
2. **A small type scale beats a large one.** Five to eight sizes total, derived from a ratio (1.125, 1.2, 1.25, 1.333, 1.414, 1.5, 1.618). Freeform sizes are a tell.
3. **Optical sizing matters at the extremes.** Display sizes (≥40px) want tighter letter-spacing and tighter line-height. Body sizes (14-18px) want their defaults. Caption sizes (≤13px) want slightly looser tracking. Variable fonts with an `opsz` axis do this automatically; static fonts need manual adjustment.
4. **Line-length is a comprehension lever.** 45-75 characters per line for body prose, narrower for poetry and citation, wider only when the design language allows it. Beyond 80ch, comprehension drops.
5. **Numerics deserve their own attention.** Tabular figures for tables and dashboards, proportional figures for prose. Old-style figures for editorial body, lining figures for UI. Slashed zero where ambiguity matters (file paths, IDs).

## Choosing type

- **Sans serifs** for screens, dense interfaces, and modern voice. Inter, Söhne, ABC Diatype, GT America, Untitled Sans, Helvetica Now, system-ui. Inter is the safest default; the others carry character if you can license them.
- **Serifs** for editorial, long-form, or product names that need warmth. Fraunces, Tiempos Text, GT Sectra, Newsreader, Source Serif, EB Garamond.
- **Slab serifs** for industrial, mechanical, or playful surfaces. Roboto Slab, IBM Plex Serif, Archivo.
- **Monospace** for code, data, technical labels, timecodes, IDs. JetBrains Mono, IBM Plex Mono, Berkeley Mono, Söhne Mono.
- **Variable fonts** where possible. One file, infinite weights, plus axes for optical size, width, and (in Fraunces, Recursive, etc.) personality. They are the modern default.

## Pairing

The most common workable pairings, in order of safety:

1. **One sans, everything.** A single excellent sans across display, body, and UI. Inter alone, used well, beats most pairings.
2. **Sans + mono.** Sans for content, mono for code, IDs, timecodes, technical labels.
3. **Serif + sans.** Serif for display or editorial body, sans for UI and metadata. The classic editorial pair.
4. **Serif + serif** (same superfamily). E.g. Fraunces Display + Fraunces Text. The most refined pair, but requires the superfamily to exist.

Mixing two random sans-serifs or two random serifs almost never works. If you must, ensure they have different proportions (one humanist, one geometric).

## Scale

A starting type scale, ratio 1.25:

| Token | Size | Use |
|---|---|---|
| xs | 12px | metadata, captions, legal |
| sm | 14px | secondary UI, helper text |
| base | 16px | body, UI |
| lg | 20px | emphasis, lead paragraphs |
| xl | 24px | small headings, card titles |
| 2xl | 32px | section headings |
| 3xl | 40px | page titles |
| 4xl | 56px | hero |
| 5xl | 72px | display hero, editorial cover |

Tune the ratio for the project: tighter (1.125) for dense tools, looser (1.414) for editorial.

## Weight

- **4-5 weights maximum** across the system. A common kit: 400 (regular), 500 (medium for UI emphasis), 600 (semibold for UI strong), 700 (bold for headings), and optionally 300 (light for large display).
- **Body in 400 or 500.** Below 400 reads thin on most screens; above 500 reads heavy for prose.
- **Heading weight depends on aesthetic.** Editorial: lighter (400-500) at large sizes. Industrial/brutalist: heavier (700-900). Consumer: medium (600).

## Line-height (leading)

- Display (≥40px): 1.0-1.15. Tight, almost touching.
- Subheads (24-36px): 1.2-1.3.
- Body (15-18px): 1.5-1.6.
- Long-form reading: 1.6-1.75.
- UI labels and buttons: 1.0-1.2 (since they are usually single-line).

## Letter-spacing (tracking)

- Display: -0.01 to -0.03em. Tighten as size increases.
- Body: 0. Browsers' defaults are usually correct.
- All-caps: +0.04 to +0.12em. Caps need air.
- Small caps: +0.02 to +0.05em.

## Italic and emphasis

- **Real italics, not synthetic obliques.** Most variable fonts ship a true italic; use it. Check the font's `font-style: italic` actually loads a different file.
- Italics for: titles of works, foreign words, technical terms on first mention, voice shifts in prose, emphasis when bold would be too loud.
- Avoid underlines for emphasis (reserved for links). Avoid all-caps for emphasis in body prose (it shouts).

## Numerics

- `font-feature-settings: 'tnum'` for tabular numbers (tables, dashboards, prices in a list).
- `font-feature-settings: 'lnum'` for lining figures (UI), `'onum'` for old-style figures (editorial body).
- `font-feature-settings: 'zero'` for slashed zero where 0/O ambiguity matters.
- `font-variant-numeric: tabular-nums` is the modern CSS way to express tabular.

## Hierarchy in long-form

For documents, articles, essays, and editorial pages:

- One H1 per page, at display size.
- H2 for major sections, distinctly smaller than H1.
- H3 for subsections, distinctly smaller than H2 but still clearly heading-weight.
- Avoid H4+ unless the document genuinely needs it. Three levels is usually enough.
- Drop caps and small caps at section starts where the aesthetic warrants (editorial, manuscript).
- Hung punctuation: opening quotes, periods, and hyphens hang outside the column edge. Setting: `hanging-punctuation: first last` (with safari fallback).

## Hierarchy in UI

- Page title at the top of the type scale, but not necessarily display-size. UI titles are often 24-32px, not 56px.
- Section labels in all-caps, smaller, tracked. These are signposts, not content.
- Body and metadata distinguished by colour as much as size: body in foreground, metadata at 60-70% opacity.

## Motion typography

For animated type (Remotion, motion graphics, hero sequences):

- **Mask the type, do not opacity-fade it.** A clip-path reveal from below reads as intentional; a fade-in reads as a load state.
- **Stagger by character or word, not letter-by-letter unless the piece warrants it.** Letter-by-letter is a strong choice; use it once per piece, not on every heading.
- **Easing curves matter more for type than for shapes.** Type reveals want sharp ease-out at the start (the type appears decisively) and slow finish (it settles). `cubic-bezier(0.16, 1, 0.3, 1)` is a strong default.
- **Hold the type still long enough to be read.** Display type wants at least 1.5-2 seconds visible. Motion graphics that flash type for 400ms before changing are exhausting.

## What to verify before declaring typography done

- Is the type scale limited to 5-8 sizes derived from a single ratio?
- Are no more than 2 type families in use (3 if mono is separate)?
- Are weights limited to 4-5 across the system?
- Are line-heights set per size, not globally?
- Are tabular numbers enabled in tables and dashboards?
- Does long-form prose sit at 45-75 characters per line?
- At display sizes, has letter-spacing been tightened?
- Are real italics loading, not synthetic obliques?
