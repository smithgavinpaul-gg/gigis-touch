# Sourcing — Patterns, Textures, Ornament, Reference

Where to pull primary source material from when a brief calls for patterns, textures, decorative ornament, period typography, or a specific historical aesthetic. This file is the antidote to "I'll grab something from Google Images" — the references below are deeper, better-curated, and (mostly) cleanly licensed.

## Core positions

1. **Go upstream of Pinterest.** Pinterest is downstream of museum collections. Skip the middleman, go to the source. The metadata, resolution, and rights story is better.
2. **Inspiration is free; assets are not.** Looking at a copyrighted object to inform your decisions is fine. Pixel-tracing or directly reusing it is a different category. Confirm the licence before any asset enters production.
3. **Recreate the *logic*, not the artefact.** When a wallpaper or textile motif inspires a background pattern, build the pattern yourself in SVG using its repeat structure and visual rhythm. The result is licensable, scalable, and yours.
4. **Period work ages better than trend work.** Sampling from a 1925 Soviet poster or a 1780 chinoiserie wallpaper gives the work a depth that trend-following can't. The historical vocabulary has been pressure-tested for a century.
5. **Build a personal reference library.** When you find an object that's useful, save the metadata (artist, date, museum, object ID, licence). The same object will be useful again on a different brief.

## The three primary collections

These three cover most of the use cases for a working digital designer. Each has a distinct strength.

### 1. Rijksmuseum (Amsterdam) — Rijksstudio

URL: https://www.rijksmuseum.nl/en/collection
Rijksstudio: https://www.rijksmuseum.nl/en/rijksstudio
Data portal: https://data.rijksmuseum.nl/

**Scope.** 800,000 objects with metadata. 600,000 high-resolution images.

**Licence.** The majority of digitised works are in the public domain. The Rijksmuseum explicitly permits download and reuse for personal and commercial purposes. Metadata and photography are CC-BY. (Always verify the licence on the specific object's page before commercial reuse.)

**Image delivery.** IIIF (via iiif.micr.io). High-resolution downloads available. The "deep zoom" on the site is excellent for sampling texture detail.

**API.** Open API available since 2013. Bulk data downloads exist.

**Use this for:**
- High-resolution photographic textures of real materials. Crops of paintings can supply paper, canvas, metal, ceramic, fabric, wood, and stone textures that are public-domain and ready to overlay.
- Dutch print tradition: ornamental prints, woodcuts, etchings. Sample for decorative borders, dingbats, vignette frames.
- Watercolours and drawings as colour-palette sources. Old paint samples are warmer and more nuanced than digital eyedropper colour wheels.
- Detailed botanical illustrations (use as the basis for SVG flora ornaments).

### 2. Cooper Hewitt (Smithsonian Design Museum, New York)

URL: https://collection.cooperhewitt.org/
Smithsonian Open Access (for CC0 status): https://www.si.edu/openaccess
Developer portal: https://collection.cooperhewitt.org/developers

**Scope.** 215,000+ objects across 30 centuries of design.

**Departments.**
- Drawings, Prints, and Graphic Design (~128,900 objects — the largest holding, including posters and graphic design)
- Product Design and Decorative Arts (~33,000 — ceramics, furniture, metalwork, glass, jewelry, lighting)
- Textiles (~26,000)
- Wallcoverings (~10,000 — handprinted to mass-produced wallpapers)
- Digital (typefaces, emoji, data visualisations, interactive works — unusual and underused)

**Licence.** Many objects participate in Smithsonian Open Access, which is CC0. Check the specific object's page or filter via si.edu/openaccess to confirm before commercial use.

**API.** REST API at api.collection.cooperhewitt.org/rest/. OAuth 2.0. The museum has historically open-sourced data and tooling on GitHub.

**Use this for:**
- The largest single archive of design-specific patterns. The Wallcoverings and Textiles departments are the standout for backgrounds, decorative panels, and repeat motifs.
- Decorative ornament, frames, cartouches, dingbats. Trace as SVG for section breaks, drop-cap surrounds, footer ornaments.
- Historical graphic design and poster vocabulary across the full Drawings/Prints department.
- The Digital department is a quietly valuable resource for thinking about contemporary typographic and interactive work as part of a continuous design tradition.

### 3. The Wolfsonian-FIU (Miami)

URL: https://wolfsonian.org/research/collection/
Digital catalogue: https://digital.wolfsonian.org/ (and objects.wolfsonian.org)

**Scope.** 200,000+ objects.

**Focus.** "The modern age, 1850 to 1950." Fine, decorative, propaganda, and graphic arts; industrial design. Strongest in Germany, Italy, the Netherlands, and the Soviet Union — the heartland of Bauhaus, Italian Futurist, Art Deco, Soviet Constructivist, and the propaganda graphic traditions on either side of two world wars.

**Object types.** Posters, books, ephemera, archives, design drawings, furniture, paintings, sculpture, glass, textiles, ceramics, lighting, appliances.

**Licence.** Not open access. Image reuse is via permission from their Image Rights and Reproductions office. **Treat this collection as visual reference only, not as an asset library.**

**Use this for:**
- Studying the *vocabulary* of a specific period when a brief calls for it. "Make this feel Bauhaus" or "1920s Soviet poster energy" or "Art Deco hotel" gain real depth when sourced from primary objects of the period, not from third-hand Google-image hand-me-downs.
- Period typography proportions, weight, ornamental conventions.
- Propaganda graphic discipline: bold geometry, restrained palette, monumental scale, message hierarchy. Lessons translate directly to modern poster and editorial work.
- Industrial design silhouettes when designing icons or product illustrations in a period-aligned style.

## How to leverage these collections in practice

A working translation from museum object to design output. Each pattern below is the move; the source is the inspiration, not the deliverable.

### Patterns and repeating backgrounds

1. **Browse a wallpaper or textile department** (Cooper Hewitt Wallcoverings and Textiles are dense gold mines; Rijksmuseum has Dutch decorative prints).
2. **Identify the repeat unit.** Most wallpapers and textiles have a small tile that repeats. Find it.
3. **Sketch the repeat structure as SVG.** A `<pattern>` element with the motif placed once, set to repeat. You now have a tileable background sized to any container.
4. **Adjust colour, scale, and contrast** to the project's palette. The historical object set the *rhythm*; you set the *voice*.

### Textures (paper, metal, fabric, ceramic)

1. **Find a Rijksmuseum painting close-up.** Sample paper from a still life background, metal from a Vermeer brass pitcher, ceramic from a delftware tile, fabric from a portrait sitter's coat.
2. **Crop tight to a flat area** of the material. Save as a high-res image.
3. **Convert to a low-opacity overlay** (15–30%) at multiply or overlay blend mode. The page now sits on a real material instead of pure white.
4. **Resolution matters.** Use the highest IIIF crop available; downscaling preserves grain. Upscaling destroys it.

### Decorative ornament (dingbats, drop-cap surrounds, frames)

1. **Cooper Hewitt's Drawings/Prints department** has tens of thousands of decorative graphic elements: borders, cartouches, ornamental initials, vignettes.
2. **Trace as SVG**. Hand-trace in Figma/Illustrator/Affinity, or use a tool like Inkscape's auto-trace as a starting point, then clean the paths.
3. **Use sparingly.** One ornament per long page is editorial discipline. Three is decoration.

### Period-accurate palettes

1. **Pick an object from the era the brief evokes** (Bauhaus poster, Memphis textile, Art Nouveau wallpaper, 18th-century French silk).
2. **Sample 5–7 colours from it** with a colour picker on the high-res image.
3. **Build the palette from those samples**, not from a generic colour-wheel exercise. Period palettes carry the period's atmosphere because they were made with that period's pigments and printing technology.

### Typography reference

1. **Period type specimens** (Rijksmuseum print holdings; Cooper Hewitt Digital department; Wolfsonian posters) are richer than the typeface preview pages on Google Fonts.
2. **Study proportions, weights, ornaments, and how the type sits with imagery.** That is the lesson, not the specific typeface name.
3. **Then pick a contemporary release that honours those proportions.** A 2024 Fraunces cut can carry the spirit of a 1790 Bodoni when the layout discipline matches.

### Studying a named aesthetic

When a brief names a style ("Swiss", "Brutalist", "Memphis", "Constructivist", "Art Deco"):

1. **Find five primary objects of the style** from the relevant collection.
2. **Identify the three rules that hold across all five.** This is the style's structural grammar.
3. **Apply those rules, not the surface details, to the new work.**

This is the difference between an authentic re-use of a tradition and a pastiche.

## The broader landscape

Other public collections worth knowing about, in order of usefulness for digital design:

- **The Met Open Access** (metmuseum.org) — 490,000+ CC0 images. Particularly strong for European decorative arts, Japanese prints, and costume.
- **Library of Congress Free to Use and Reuse** (loc.gov) — propaganda, photography, posters, type specimens, sheet music covers.
- **The Public Domain Review** (publicdomainreview.org) — curated entry-point into the wider public domain, often surfacing obscure beautiful work.
- **Wellcome Collection** (wellcomecollection.org) — medical, botanical, anatomical imagery under CC-BY.
- **Internet Archive Book Images on Flickr** — 5M+ public-domain illustrations extracted from scanned books, with metadata. Hit-or-miss but occasionally extraordinary.

Use these to supplement the three primary collections, not replace them. The primaries are deep enough that most briefs find what they need there.

## Licence discipline

A short, working policy:

- **CC0 / Public Domain**: free to reuse, even commercially. Verify per object.
- **CC-BY**: free to reuse, with attribution. Credit the museum and the artist.
- **All Rights Reserved / "Image Rights" required**: visual reference only. Do not redistribute the source image, and do not pixel-trace into deliverables. Inspiration is allowed; copying is not.
- **When in doubt**: assume restricted. Build the asset yourself, informed by what you saw.

A useful test: if the client received a cease-and-desist over the asset, could you explain the provenance and show it's clean? If yes, ship. If no, recreate.

## What to verify before declaring sourcing done

- Did you find at least three primary references from the collections above, not from a Pinterest board?
- Did you record the source (museum, object ID, licence) for each reference?
- For any asset that entered the deliverable: have you confirmed the licence permits commercial use, or did you recreate it from scratch?
- Does the work read as informed by primary sources, or could it have been made by anyone with a Pinterest account?
- Have you applied the *grammar* of the reference (structure, palette, rhythm), not just the surface?
