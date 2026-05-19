---
name: gigis-touch
description: A comprehensive, principles-only design skill for digital product work, synthesised from the leading open-source Claude Code design skills (frontend-design, ui-ux-pro-max, taste, LibreUIUX, designer-skills, motion-dev, remotion-superpowers, css-animation, open-design, tailwindcss-marketplace, mobile-app-design, code-architect, and the awesome-claude-skills directories). Use whenever you are designing, building, refining, reviewing, or critiquing any digital interface, motion piece, video, mobile screen, or visual system. The principles are framework-agnostic and platform-agnostic; they apply equally to web, mobile, video, and prototype work.
metadata:
  version: "1.0.0"
  scope: universal
---

# Gigi's Touch

A big-picture design skill. The goal is not to enforce one aesthetic, but to apply *principles that hold across aesthetics* so that whatever you build is intentional, refined, and honest to its medium.

Treat this skill as a checklist of disciplines to consult, not a style guide to obey. The strongest design decisions usually come from picking the right discipline to lean into for the moment, then executing it cleanly.

## When to invoke

Reach for this skill on any of:

- Building a new interface, screen, page, or component from scratch.
- Refining or polishing an existing surface.
- Designing motion, video, transitions, or animations.
- Reviewing or critiquing a design (your own or someone else's).
- Translating a brief, mood, or reference into working code.
- Picking type, colour, spacing, or motion vocabulary.
- Deciding whether something is *done* or still needs work.

If the task is purely structural code (no surface impact, no user-facing artifact), this skill is not the right tool, use the relevant engineering skill instead.

## Foundational stance (read this every invocation)

These are the cross-cutting positions the rest of the skill is built on.

1. **Intent before pixels.** Before any visual decision, articulate *what the surface is for* and *who it is for*. A landing page sells, a tool persists, an editorial piece is read, a video is watched, a documentation page is searched. The medium dictates the rules.
2. **Decisions, not defaults.** Every visible property (type size, colour, spacing, corner radius, easing, weight) is a decision. Inherited defaults are decisions you have not yet made. Audit your defaults before shipping.
3. **Consistency over novelty, except where novelty is the point.** Most parts of a product should be familiar; one or two parts can be distinctive. Reverse this and the product becomes exhausting; over-do it and it becomes invisible.
4. **Constraints are the source of taste.** A reduced palette, a tight type scale, a small motion vocabulary, a chosen grid — these are not limitations, they are what make the work cohere. Add elements reluctantly; remove them eagerly.
5. **Refinement is mostly subtraction.** When a piece feels "off", the answer is more often *less* (fewer fonts, fewer colours, fewer effects, fewer words) than *more*. If you cannot identify the one element doing the most work, you have not refined far enough.
6. **Verify in context.** A component looks one way in Storybook, another in the page, a third on a 13" laptop with low brightness, a fourth on a phone in daylight. Designs are not done until they have been seen in the contexts they will live in.
7. **Don't impersonate an aesthetic you don't understand.** "Make it Swiss", "make it editorial", "make it brutalist" without understanding the history and constraints of those traditions produces parody. If you reach for a named style, look at primary references first.
8. **Resist the AI-generic.** Purple-to-pink gradients, rounded-2xl blob cards, three-column feature grids with Lucide icons, hero with a screenshot floating at 8 degrees, "powered by" footers — these are the AI fingerprint. They are not wrong, they are *worn out*. Reach past the first idea.

## Principle domains

The skill is organised into eleven principle domains. For any task, pull the two or three most relevant.

| Domain | When to read | File |
|---|---|---|
| User experience | Information architecture, task flows, copy as UX, error states, empty states, accessibility intent | `principles/ux.md` |
| User interface | Components, controls, states, hierarchy, density, affordance, feedback | `principles/ui.md` |
| Typography | Type scales, pairings, optical sizing, kerning, line-length, rhythm, numeric features | `principles/typography.md` |
| Colour | Palettes, accent discipline, contrast, dark/light, semantic colour, gradients | `principles/color.md` |
| Layout & grid | Grid systems, asymmetry, whitespace, hierarchy, baseline rhythm, responsive logic | `principles/layout-grid.md` |
| Motion | Easing, duration, choreography, scroll behaviour, page transitions, micro-interactions | `principles/motion.md` |
| Texture & material | Grain, noise, paper, halftone, depth, light, shadow, surface | `principles/texture.md` |
| Taste & references | How to avoid AI-generic output, how to study references, where good work lives | `principles/taste.md` |
| Accessibility | Contrast, focus states, motion-reduction, semantic HTML, keyboard, screen reader, cognitive load | `principles/accessibility.md` |
| Architecture (design-side) | Component hierarchy, token systems, design-engineering boundary, naming, file structure | `principles/architecture.md` |
| Mobile & native | Touch targets, gestures, safe areas, native conventions, platform respect | `principles/mobile-native.md` |

## Stack guidance

Principles realised through a stack. These files translate the principles above into the specific tools they are usually built with.

- `stacks/tailwind.md` — utility-first CSS, token strategy, when to escape the system
- `stacks/remotion.md` — programmatic video, composition design, timing as rhythm
- `stacks/css-motion.md` — animation in plain CSS, transitions vs animations, will-change discipline
- `stacks/component-libraries.md` — working with shadcn, Radix, Headless UI, MUI, Mantine without inheriting their generic surface

## Workflow

The same principles, applied as process.

- `workflow/before-you-code.md` — the read-the-room checklist that runs *before* you write a line
- `workflow/design-review.md` — a structured critique format for self-review or peer review
- `workflow/refinement.md` — how to take a surface from "working" to "done"

## How to use this skill in a conversation

1. Read this file (the index) on every invocation.
2. Identify the task type and the medium.
3. Open `workflow/before-you-code.md`.
4. Pull two or three relevant principle files for the task at hand. Do not pull everything; pull what applies.
5. If a stack is named in the task, open the relevant stack file.
6. Make your decisions deliberately. State the read-back (what you understand, what you'll do, what you'll deliberately not do) before producing code.
7. Before declaring the work done, open `workflow/design-review.md` and run the check.

## Lineage

This skill is a synthesis of community thinking. The principle domains and their structure draw on:

- **Foundational design skills**: Anthropic's `frontend-design` plugin, `ui-ux-pro-max-skill`, `taste-skill`, `Claude-Code-Frontend-Design-Toolkit`.
- **UX**: `designer-skills`, `bencium-claude-code-design-skill`, `claude-code-ui-agents`.
- **UI**: `LibreUIUX-Claude-Code`, `interface-design`, `claude-design-skill`.
- **Software design**: `claude-code-templates`, `code-architect` agent, `claude-code-ultimate-guide`, `claude-code-from-source`, `Dive-into-Claude-Code`.
- **Design inspiration**: `frontend-design-pro-demo`, `Ilm-Alan/frontend-design`, `claude-frontend-skills`.
- **Textures**: `claudedesignskills`, `jezweb/claude-skills`, Anthropic's `skills` (algorithmic-art, canvas-design, brand-guidelines).
- **Remotion**: `remotion-superpowers`, `Claude-Code-Video-Toolkit`, `everything-claude-code`, `remotion-video-skill`, `claude-code-skills-lab`, `remotion-claude-video`, Remotion's official Claude Code guide.
- **Motion**: `motion-dev-animations-skill`, `wiggle-claude-skill`, `css-animation-skill`.
- **Typography**: `open-design`, `glebis/claude-skills`.
- **Tailwind**: `claude-code-kit`, `secondsky/claude-skills`, `tailwindcss-marketplace`, `flyingwebie/claude-agents`, `sveltekit-svelte5-tailwind-skill`.
- **Mobile & native**: `mobile-app-ui-design`, `awesome-skills/mobile-app-design`, `claude-android-skill`.

What is kept here is the *principle behind the technique*, not the technique itself. Specific patterns date quickly; the principles last.
