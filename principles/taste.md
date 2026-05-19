# Taste & References

Synthesised from the `taste-skill`, the design-inspiration repos, and the "avoid AI-generic" thread that runs through all the foundational frontend skills.

Taste is the ability to recognise *which idea is better* without being able to fully articulate why. It is built through exposure to good work, attention to detail, and the discipline to discard your first idea.

## Core positions

1. **The first idea is rarely the best.** AI systems and human designers alike default to the most common pattern. The strongest work comes from rejecting the first idea and reaching for the second or third.
2. **Generic is the enemy.** A piece that could have been made by anyone, for anyone, is forgettable. Specificity (to the brand, the content, the moment) is what makes work memorable.
3. **References, not templates.** Study how strong work is *made*, not just what it looks like. Copy the principle, not the surface.
4. **Taste is local.** Good work in one context (a brutalist gallery site) is wrong in another (a banking app). Taste is not a single dial labelled "more design"; it is many dials, calibrated per context.
5. **Showing your work means making clear choices.** A design that wavers between three references reads as confused. Pick one direction and execute it cleanly.

## The AI-generic fingerprint

These patterns are not wrong, they are *worn out*. They appear in roughly 80% of AI-generated frontends and have become invisible.

**Visual tells:**
- Purple-to-pink gradient backgrounds, especially radial mesh blobs.
- Rounded-2xl (16px) corner radius on everything.
- Drop-shadow-2xl floating cards on the hero.
- Three-column feature grids with one-icon-one-headline-three-lines.
- Stripe-clone hero: large text left, browser window screenshot right.
- Lucide icons at default 2px stroke, centred above a feature title.
- Light grey backgrounds (#F9FAFB) with white cards on top.
- Indigo, violet, or fuchsia as primary accent.
- "Built with [tech]" badges in the footer.
- Glassmorphism on navigation bars.

**Structural tells:**
- Hero → Features → Testimonials → CTA → Footer, on every page.
- "Trusted by" logo strip immediately under hero.
- FAQ accordion with 6-8 questions, all in the same tone.
- "How it works" with three numbered steps.
- Pricing with three tiers labelled "Starter / Pro / Enterprise".
- Avatar circles with random unsplash faces in testimonials.

**Copy tells:**
- "Built for the modern team."
- "The future of [X]."
- "Powerful. Simple. Beautiful."
- "Get started in seconds."
- "Loved by thousands of [users]."
- "Trusted by industry leaders."
- Em dashes — placed — like — this — throughout — copy. Em dashes are useful in prose; their overuse is the single strongest "AI wrote this" tell.

**Motion tells:**
- Fade-in-on-scroll for every paragraph.
- Hover scale 1.05 on every card.
- A continuously animating SVG blob behind the hero.
- 0.3s ease-in-out as the universal transition for everything.

## How to escape

For each generic pattern, the principle behind it suggests alternatives:

| Generic | The thing it's trying to do | Less-tired alternative |
|---|---|---|
| Purple-pink gradient | Energetic feel | A single saturated accent on a neutral, or a duotone photo |
| Rounded-2xl everything | Friendly feel | Mixed radii (sharp containers, soft buttons) or all-sharp + warm palette |
| Drop-shadow-2xl floating | Suggest depth | Hairline border + slightly elevated surface colour |
| 3-column feature grid | Show product breadth | Long-form narrative with embedded screenshots, or a wide bento with varied sizes |
| Stripe-clone hero | Show product context | A typographic hero with no product shot, or full-bleed photography |
| Lucide @ 2px default | Visual aid | Custom icons, or heavier stroke, or no icons (just labels) |
| Light grey + white cards | Soft layering | Single canvas + hairline borders + considered whitespace |
| Indigo/violet accent | Modern tech feel | A more specific hue chosen for the brand (forest green, oxblood, ochre, electric blue) |

## How to study references

When given a reference (Awwwards, Brutalist Websites, Siteinspire, Designspiration, Codrops, Cosmos, Are.na), study it on three levels:

1. **What is the surface doing?** Type choices, palette, layout, motion. Observable facts.
2. **Why is that surface doing that?** What is it communicating about the product, brand, or moment? What would change if you removed one element?
3. **What is the underlying principle?** "It's centred-asymmetric" is surface. "It's centred-asymmetric because the content is poetry and poetry has implicit centring but explicit asymmetry" is principle.

Take the principle into your work. Avoid copying the surface; the principle will produce a different surface in a different context, which is correct.

## Where to look

Strong work lives in roughly these places (in 2026):

- **Cosmos** (cosmos.so) — curated visual references, less SaaS-leaning than Awwwards.
- **Are.na** (are.na) — long-tail design research, curators with strong specific taste.
- **SiteInspire** (siteinspire.com) — curated, varied, fewer fads.
- **Brutalist Websites** (brutalistwebsites.com) — niche, but useful as a counterweight.
- **Designspiration** (designspiration.net) — broad graphic design beyond web.
- **The Webby Awards** and **D&AD** — historical, slower-moving, less trend-driven.
- **Print archives**: AIGA, Eye Magazine, Idea Magazine. Print design is older and the lessons are deeper.
- **Specific studios' sites**: Pentagram, Mucca, Order, Manual, Bielke&Yang, Hoffmann Angelic. Studio sites are usually a master class in restraint.

Awwwards is a useful but biased mirror. Its winners trend towards motion-heavy, scroll-jacked, kinetic-typography pieces that win awards but lose users. Treat it as inspiration for *moments* of motion, not as a model for *whole products*.

## Anti-aesthetic taste

Some products should look *deliberately* boring. A banking app, a medical record system, a tax filing tool. Taste in these contexts means restraint, predictability, and respect for the user's time. The temptation to inject "delight" usually backfires. Confidence in boring is a form of taste.

## Reading the brief

Most failures of taste happen at the brief stage:

- Did you understand what the user is for? (Tool? Toy? Reference? Sales surface?)
- Did you understand the brand's existing voice? Or were you free to invent one?
- Did you understand the audience? (Industry professionals? General consumers? Children?)
- Did you understand the context of use? (Long sittings? Quick glances? On-the-go phones?)

A "make it pretty" request is incomplete. Re-read the brief and articulate the answers above before producing anything.

## Read-back protocol

Before producing any design work, state:

> "I read this as a [tool / editorial / marketing / utility / brand] surface for [audience]. The brief implies [voice / mood]. I will lean into [one specific direction]. I will deliberately avoid [the obvious AI-generic pattern that this brief would otherwise produce]."

Then proceed. The read-back is a forcing function for taste.

## What to verify before declaring taste-checks done

- Have you audited the work against the AI-generic fingerprint list above?
- Did you write a read-back before starting?
- Did you pick one direction, not three?
- Have you avoided em dashes in any copy?
- Have you removed every "Built with", "Powered by", "Trusted by" pattern unless genuinely warranted?
- Is the work specific enough that it could only be this product, not any product?
