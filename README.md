# gigis-touch

A comprehensive, principles-only Claude Code skill for digital product design.

`gigis-touch` is a single installable skill that distils the thinking from across the open-source Claude Code design ecosystem into one coherent reference. It does not aggregate code from those repos; it synthesises the *principles behind* them into framework-agnostic, platform-agnostic guidance that holds across web, mobile, video, and prototype work.

Invoke it with `/gigis-touch` in Claude Code, on any design, refinement, critique, or build task.

## What problem this solves

The open-source design-skill landscape for Claude Code is rich but fragmented. There are dozens of skills, each excellent at one slice: typography, motion, Tailwind, Remotion, UX, accessibility. Picking the right one mid-task is friction. Installing all of them is bloat. Most overlap heavily.

`gigis-touch` is one skill that:

- Covers the full surface (UX, UI, typography, colour, layout, motion, texture, taste, accessibility, architecture, mobile, Tailwind, Remotion, CSS motion, component libraries).
- Distils the *thinking* rather than the techniques, so the guidance ages well as specific tools change.
- Loads lean (SKILL.md is the index) and pulls deeper files on demand for the task at hand.
- Stays framework-agnostic. Principles apply whether you're building in Next, SvelteKit, SwiftUI, Remotion, or plain HTML.

## What it is not

- **Not a fork or aggregation.** No code from the source repos is included. This is an independent distillation under MIT.
- **Not an aesthetic prescription.** The skill does not enforce a single style. It enforces *the discipline of being deliberate about style* and provides principles for executing whichever direction is chosen.
- **Not a replacement for the source skills.** If you want one of the source skills' specific patterns, install it directly. `gigis-touch` complements them.
- **Not a personal style guide.** The first prototype of this skill was personal-DNA flavoured for one designer; this public release is universal by design.

## Install

Skills live in `~/.claude/skills/` on macOS / Linux. Clone the repo into that directory:

```bash
git clone https://github.com/smithgavinpaul-gg/gigis-touch ~/.claude/skills/gigis-touch
```

Restart your Claude Code session, or wait a moment for the skill list to refresh. `/gigis-touch` will appear in the available skills.

You can also install it under a project's local `.claude/skills/` if you want it scoped to a single repo.

## Use

In Claude Code:

```
/gigis-touch
```

The model reads `SKILL.md`, then identifies the task and pulls only the 2-3 principle files that apply. There's no need to memorise the file structure; the SKILL.md acts as a router.

Good triggers:

- "Build a hero section for this page."
- "Refine this dashboard."
- "Critique this design."
- "Pick a type system for this site."
- "Animate this modal entrance."
- "Make this Remotion piece feel less generic."
- "Audit this surface for AI-generic tells."

## Structure

```
gigis-touch/
├── SKILL.md                          # master index, foundational stance, mode router
├── principles/                       # 11 cross-cutting principle domains
│   ├── ux.md
│   ├── ui.md
│   ├── typography.md
│   ├── color.md
│   ├── layout-grid.md
│   ├── motion.md
│   ├── texture.md
│   ├── taste.md
│   ├── accessibility.md
│   ├── architecture.md
│   └── mobile-native.md
├── stacks/                           # principles through specific tools
│   ├── tailwind.md
│   ├── remotion.md
│   ├── css-motion.md
│   └── component-libraries.md
└── workflow/                         # principles as process
    ├── before-you-code.md
    ├── design-review.md
    └── refinement.md
```

Each file follows the same shape: core positions, then concrete sub-principles with examples, ending with a verification checklist so the work can be self-audited.

## Foundational stance

Eight cross-cutting positions sit at the top of `SKILL.md`, applied to every task:

1. Intent before pixels.
2. Decisions, not defaults.
3. Consistency over novelty, except where novelty is the point.
4. Constraints are the source of taste.
5. Refinement is mostly subtraction.
6. Verify in context.
7. Don't impersonate an aesthetic you don't understand.
8. Resist the AI-generic.

The full reasoning is in `SKILL.md`.

## Lineage and source attribution

`gigis-touch` is a synthesis. The thinking comes from the following community skills, articles, and projects. None of their code is included; their *thinking* shaped this skill.

### Foundational / all-rounders

- [anthropics/claude-code — frontend-design plugin](https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design)
- [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
- [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill)
- [wilwaldon/Claude-Code-Frontend-Design-Toolkit](https://github.com/wilwaldon/Claude-Code-Frontend-Design-Toolkit)

### UX

- [Owl-Listener/designer-skills](https://github.com/Owl-Listener/designer-skills)
- [bencium/bencium-claude-code-design-skill](https://github.com/bencium/bencium-claude-code-design-skill)
- [mustafakendiguzel/claude-code-ui-agents](https://github.com/mustafakendiguzel/claude-code-ui-agents)

### UI

- [HermeticOrmus/LibreUIUX-Claude-Code](https://github.com/HermeticOrmus/LibreUIUX-Claude-Code)
- [Dammyjay93/interface-design](https://github.com/Dammyjay93/interface-design)
- [jiji262/claude-design-skill](https://github.com/jiji262/claude-design-skill)

### Software design / architecture

- [davila7/claude-code-templates](https://github.com/davila7/claude-code-templates)
- [anthropics/claude-code — feature-dev / code-architect agent](https://github.com/anthropics/claude-code/blob/main/plugins/feature-dev/agents/code-architect.md)
- [FlorianBruniaux/claude-code-ultimate-guide](https://github.com/FlorianBruniaux/claude-code-ultimate-guide)
- [alejandrobalderas/claude-code-from-source](https://github.com/alejandrobalderas/claude-code-from-source)
- [ComeOnOliver/claude-code-analysis](https://github.com/ComeOnOliver/claude-code-analysis)
- [VILA-Lab/Dive-into-Claude-Code](https://github.com/VILA-Lab/Dive-into-Claude-Code)
- [levnikolaevich/claude-code-skills](https://github.com/levnikolaevich/claude-code-skills)

### Design inspiration

- [claudekit/frontend-design-pro-demo](https://github.com/claudekit/frontend-design-pro-demo)
- [Ilm-Alan/frontend-design](https://github.com/Ilm-Alan/frontend-design)
- [Koomook/claude-frontend-skills](https://github.com/Koomook/claude-frontend-skills)
- [claudekit/frontend-design-pro-demo (live gallery)](https://claudekit.github.io/frontend-design-pro-demo)

### Textures / visual resources

- [freshtechbro/claudedesignskills](https://github.com/freshtechbro/claudedesignskills)
- [jezweb/claude-skills](https://github.com/jezweb/claude-skills)
- [anthropics/skills (official; algorithmic-art, canvas-design, brand-guidelines)](https://github.com/anthropics/skills)

### Remotion

- [DojoCodingLabs/remotion-superpowers](https://github.com/DojoCodingLabs/remotion-superpowers)
- [wilwaldon/Claude-Code-Video-Toolkit](https://github.com/wilwaldon/Claude-Code-Video-Toolkit)
- [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code)
- [wshuyi/remotion-video-skill](https://github.com/wshuyi/remotion-video-skill)
- [panaversity/claude-code-skills-lab](https://github.com/panaversity/claude-code-skills-lab)
- [JJenglert1/remotion-claude-video](https://github.com/JJenglert1/remotion-claude-video)
- [Remotion docs — Claude Code guide](https://www.remotion.dev/docs/ai/claude-code)

### Motion design

- [199-biotechnologies/motion-dev-animations-skill](https://github.com/199-biotechnologies/motion-dev-animations-skill)
- [talknerdytome-labs/wiggle-claude-skill](https://github.com/talknerdytome-labs/wiggle-claude-skill)
- [neonwatty/css-animation-skill](https://github.com/neonwatty/css-animation-skill)

### Typography and motion typography

- [nexu-io/open-design](https://github.com/nexu-io/open-design)
- [glebis/claude-skills](https://github.com/glebis/claude-skills)

### Tailwind CSS

- [blencorp/claude-code-kit](https://github.com/blencorp/claude-code-kit)
- [secondsky/claude-skills](https://github.com/secondsky/claude-skills)
- [rdimascio/tailwindcss-marketplace](https://github.com/rdimascio/tailwindcss-marketplace)
- [flyingwebie/claude-agents](https://github.com/flyingwebie/claude-agents)
- [claude-skills/sveltekit-svelte5-tailwind-skill](https://github.com/claude-skills/sveltekit-svelte5-tailwind-skill)

### App design (mobile / native)

- [ceorkm/mobile-app-ui-design](https://github.com/ceorkm/mobile-app-ui-design)
- [awesome-skills/mobile-app-design](https://github.com/awesome-skills/mobile-app-design)
- [dpconde/claude-android-skill](https://github.com/dpconde/claude-android-skill)

### Meta-lists / directories

- [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills)
- [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)
- [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)
- [BehiSecc/awesome-claude-skills](https://github.com/BehiSecc/awesome-claude-skills)
- [rohitg00/awesome-claude-code-toolkit](https://github.com/rohitg00/awesome-claude-code-toolkit)
- [abubakarsiddik31/claude-skills-collection](https://github.com/abubakarsiddik31/claude-skills-collection)

### Reference reading

- [Pasquale Pillitteri — Claude Code Skills design UI/UX guide](https://pasqualepillitteri.it/en/news/576/claude-code-skills-design-uiux-guide)
- [Snyk — Top Claude skills for UI/UX engineers](https://snyk.io/articles/top-claude-skills-ui-ux-engineers/)
- [Composio — Top design skills](https://composio.dev/content/top-design-skills)
- [AY Automate — Best Claude Code GitHub repos](https://www.ayautomate.com/blog/best-claude-code-github-repos)

If you maintain one of these projects and want the attribution adjusted (different name, removal, link to a fork), open an issue or PR.

## Contributing

The skill is intentionally opinionated. Pull requests are welcome for:

- Sharpening principles (better examples, clearer phrasing, evidence-backed claims).
- Adding stacks that genuinely earn their place (SwiftUI, Jetpack Compose, Three.js, Svelte, Flutter).
- Fixing inaccuracies, broken links, or factual drift.

Less welcome:

- Adding personal-aesthetic prescriptions (the skill is principles-only by design).
- Expanding scope into unrelated engineering territory.
- Bringing back trends already in the AI-generic fingerprint list.

## License

MIT. See [LICENSE](./LICENSE).

The included guidance is a synthesis under fair-use and independent authorship. The source repos remain under their own licenses; nothing from them is redistributed here.

## Acknowledgements

This skill exists because the open-source Claude Code design community publishes generously. Thank you to every author in the lineage list above.
