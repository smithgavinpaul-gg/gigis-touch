# Before You Code

The read-the-room checklist that runs before any visual code is written. Synthesised from the foundational frontend skills and the architectural discipline of the software-design repos.

This is the most-skipped step in design work, and the most expensive when skipped. Five minutes of reading the room saves an hour of misaligned work.

## The protocol

Run these steps in order. Do not skip any. Do not start writing code until each is answered.

### 1. Read the brief

If a brief exists (a Linear ticket, a Figma file, a comment, a paragraph in chat), read it twice.

Ask:

- What is the surface for?
  - **Tool** — used repeatedly to accomplish a task. Optimise for speed and clarity.
  - **Editorial** — read once or sparsely. Optimise for reading flow and considered detail.
  - **Marketing** — convert a visitor into an action. Optimise for clarity of value and a single CTA.
  - **Brand** — convey identity. Optimise for distinctiveness and memorability.
  - **Utility** — accomplish a single transactional task (login, pay, confirm). Optimise for friction reduction.
- Who is the audience?
  - Industry professionals? General consumers? Existing users? First-time visitors? Specialists?
- What is the context of use?
  - Long sittings or quick glances? Desktop or mobile? In quiet focus or while distracted? In daylight or low-light?
- What is the brand's existing voice?
  - Is there one to honour, or are you free to set one?
- What's the constraint?
  - Timeline? Budget? Existing tech stack? Brand guidelines? Compliance requirements?

If the brief doesn't answer these, ask before designing. A misaligned brief is the most expensive thing to fix later.

### 2. Read the codebase

If you're adding to an existing project:

- **Find the design tokens.**
  - `tailwind.config.*`, `globals.css`, `tokens.css`, `theme.css`, `:root` declarations.
  - Note the colour palette, type scale, spacing scale, radius values, shadow tokens.
- **Find the component library.**
  - `components/`, `ui/`, `shared/`. List the components by name.
  - Note the prop APIs. A `<Button>` with `variant="primary"` is one contract; a `<Button>` with `primary` boolean prop is another. Match the existing convention.
- **Find the layout primitives.**
  - Is there a `<Stack>`, `<Cluster>`, `<Container>`? Use them.
- **Find the typography setup.**
  - Custom fonts? Variable axes? Where are font-faces declared?
- **Find the motion vocabulary.**
  - Framer Motion? GSAP? CSS animations? React Spring? Match it. Don't introduce a new motion library.
- **Read at least two existing components in full.**
  - Notice the conventions: how are variants expressed, how are states handled, how is class composition done. Mirror these.

### 3. Identify the medium

- **Web (desktop)** — keyboard + mouse, big screen, hover available. Most flexible.
- **Web (mobile)** — touch, smaller screen, no hover. Design mobile-first if mobile is primary; design responsive if mixed.
- **Native iOS / Android** — platform conventions matter. See `principles/mobile-native.md`.
- **Video (Remotion or motion graphics)** — time is the canvas. See `stacks/remotion.md`.
- **Email** — table-based, ancient HTML, minimal CSS support. A different planet.
- **Print / PDF** — fixed dimensions, no interaction, type-led.

Each medium has its own affordances, constraints, and reading patterns. Don't bring web defaults into mobile, don't bring static defaults into video.

### 4. Decide on the direction (avoid AI-generic)

Read `principles/taste.md` for the AI-generic fingerprint list. Identify which generic pattern would be the *easy* answer for this brief, and consciously decide whether to use it or reject it.

- "Hero with text left and product screenshot right" — is this the right answer, or the lazy answer?
- "Three-column feature grid with icons" — is this the right answer, or the lazy answer?
- "Purple gradient mesh background" — is this the right answer, or the lazy answer?

Sometimes the easy answer is the right answer. But it should be a chosen answer, not a default.

### 5. Pick the discipline

Based on the medium and brief, identify which principle files apply most. Don't read all of them; pick the 2-3 that matter for this task.

| Task | Primary files |
|---|---|
| Hero / landing page | `principles/typography.md`, `principles/layout-grid.md`, `principles/taste.md` |
| Dashboard / tool | `principles/ui.md`, `principles/ux.md`, `principles/layout-grid.md` |
| Editorial / long-form | `principles/typography.md`, `principles/texture.md`, `principles/layout-grid.md` |
| Mobile screen | `principles/mobile-native.md`, `principles/ux.md`, `principles/motion.md` |
| Brand site | `principles/typography.md`, `principles/taste.md`, `principles/motion.md` |
| Video / Remotion | `stacks/remotion.md`, `principles/motion.md`, `principles/typography.md` |
| Component refactor | `principles/architecture.md`, `principles/ui.md` |
| Accessibility pass | `principles/accessibility.md`, `principles/color.md`, `principles/motion.md` |

### 6. State your read-back

Before writing any code, produce a short read-back. In your own words:

- **What you understand the brief to be.** One sentence.
- **What kind of surface this is** (tool / editorial / marketing / utility / brand). One sentence.
- **The direction you're going to take.** Two sentences, including what you'll *deliberately not* do.
- **Tokens, components, and motion you'll reuse from the existing codebase.** Bullet list.

Example:

> This is a settings page for a mid-sized B2B product. It's a tool surface, used by power users repeatedly. I'll lean into information density and clear primary actions, in line with the existing dashboard pages I read in `components/dashboard/`. I'll deliberately avoid hero-style typography and excessive whitespace, which would feel wrong for this context. Reusing: existing `<Stack>`, `<FormField>`, `<Button>` (variant=primary for the save action). Following the existing token system; no new colours or spacings.

The read-back is a forcing function for clarity. It surfaces misalignment before you spend hours on the wrong thing.

### 7. Sketch before building

For non-trivial surfaces, write a structural outline before writing JSX:

```
HEADER
  - title
  - subtitle (optional)
  - primary action
SECTION 1: Account details
  - 4 fields, two per row
  - save button at section foot
SECTION 2: Notification preferences
  - 6 toggles, grouped
  - no per-section save (saved globally)
FOOTER
  - global save action
  - global cancel action
```

This is cheaper to revise than code. Once the structure is right, write the JSX.

### 8. Now you can code

After the seven steps above, you can write code. Not before.

## Why this matters

Most "the design is wrong" feedback traces back to a skipped step in this protocol. The work was technically competent but answered the wrong question, didn't fit the codebase, or hit a generic pattern that no one wanted but no one rejected.

The protocol is annoying to run. It is not optional.

## What to verify before declaring this step done

- Have you read the brief twice?
- Have you found and noted the existing tokens?
- Have you read at least two existing components?
- Have you identified the medium and its constraints?
- Have you consciously decided about the AI-generic temptation?
- Have you picked the 2-3 principle files that apply?
- Have you written your read-back?
- Have you sketched the structure?

If yes to all, you're ready to code.
