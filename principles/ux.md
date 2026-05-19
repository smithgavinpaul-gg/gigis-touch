# User Experience

Synthesised from the UX-oriented skills in the source set (`designer-skills`, `bencium-claude-code-design-skill`, `claude-code-ui-agents`, `ui-ux-pro-max`).

UX is the discipline of getting out of the user's way. It is upstream of UI: visual decisions cannot rescue an unclear task flow, a buried action, or an unkind error state.

## Core positions

1. **The product's job is the user's job done.** Every screen, control, and word should be in service of the user finishing a task. If something does not serve a task, justify it explicitly or remove it.
2. **The shortest path that does not patronise.** Reduce steps, but do not strip context the user needs to feel confident. Two well-explained steps beat one underexplained one.
3. **Match the user's mental model, then nudge it.** Use the names, metaphors, and groupings your users already use. If their model is wrong, teach it gradually through UI, not through a wall of onboarding text.
4. **State, always.** A screen has at minimum five states: loading, empty, partial, full, error. Design all of them. A product is only as polished as its weakest state.
5. **Copy is UX.** Button labels, microcopy, error messages, empty states, and toasts are not decoration; they *are* the experience for most users. Spend time on them.

## Information architecture

- **Group by user task, not internal taxonomy.** A "Settings > Billing > Subscription" hierarchy that mirrors the company org chart is a tell. Reorganise around what the user came to do.
- **Limit primary navigation.** Five to seven items in a primary nav is the practical ceiling. More than that and discovery collapses. If you exceed it, your IA is not done.
- **Disclose progressively.** Surface the 80% case; let the 20% live one level deeper. Do not punish the majority for the minority's edge cases.
- **Make hierarchy visible.** A user should be able to tell from any page: where am I, what is above me, what is around me, what is the action.

## Task flows

- **One primary action per screen.** Identify it before designing the screen. Every other action is secondary.
- **Linear when it can be, branching when it must be.** Wizards are not always wrong. A 4-step linear flow with clear progress beats a single dense form that scares people off.
- **Resumable.** Long flows must remember where the user left off. Closing the browser is not a destructive act.
- **Reversible.** Destructive actions need confirmation; near-destructive actions need undo. Confirmation modals are a tax; undo toasts are a gift.

## Forms

- **Ask only for what you need now.** Every field is a friction tax.
- **Label position**: above the field for scanability, in-field placeholders only when there is *also* a persistent label (placeholders alone fail accessibility and forget themselves after typing).
- **Validate at the right moment**: on blur for individual fields, on submit for cross-field constraints. Never validate on every keystroke unless the user is actively typing into a field that benefits (password strength, username availability).
- **Error messages**: explain *what* is wrong and *how to fix it*. "Invalid email" is bad; "Email needs to look like name@example.com" is good.
- **Group related fields**, separate unrelated ones. A form is not a CSV.

## States in detail

- **Loading**: skeleton over spinner where the shape of the eventual content is known. Spinners for genuinely uncertain durations. Show progress where you can measure it.
- **Empty**: an empty state is a *briefing*. Tell the user what would normally be here, why it's not, and what they can do to fill it. Do not show a sad face.
- **Partial**: when content is partially loaded, show what you have and indicate what's coming. Do not hold the whole page hostage to the slowest piece.
- **Error**: be specific, be kind, give an action. "Something went wrong" is malpractice; "We couldn't reach the server. Retry, or contact support if this keeps happening" is correct.
- **Success**: acknowledge what happened, then get out of the way. A success toast that lingers becomes a chore.

## Microcopy

- **Use the user's verbs.** "Save", "Send", "Pay" beat "Submit". "Continue" beats "Next" when the flow is content; "Next" beats "Continue" when the flow is wizard-like.
- **No false enthusiasm.** "Awesome!", "Great!", "Let's go!" age into condescension. Plain confirmation reads as confident.
- **No corporate hedging.** "Please be advised that...", "Kindly note...", "We regret to inform you..." are bureaucratic costumes. Speak directly.
- **Sentence case, not Title Case**, in most product UI. Title Case in product surfaces tells the user this is a Form, capital F. Sentence case feels like a tool a person designed.

## Accessibility as UX

Accessibility is not a downstream compliance pass; it is upstream task design.

- Touch targets at least 44×44px (iOS) / 48×48dp (Android) on mobile, generous click targets on web.
- Focus order matches reading order. Tab through your own page weekly.
- All interactive elements reachable by keyboard, all action states announced to screen readers.
- Reduced motion preference respected (see `principles/motion.md`).
- Colour is never the *only* carrier of information; pair with shape, icon, or text.

See `principles/accessibility.md` for the full discipline.

## Cognitive load

- **Chunking**: group like with like in 5±2 items per chunk.
- **Recognition over recall**: show options, do not require the user to remember them.
- **Defaults that fit the common case**: the default value of a setting should be what 80% of users want. The remaining 20% should still find it easy to change.
- **One decision at a time**: do not stack a paywall, a permissions prompt, and a feature tour on the same screen.

## What to verify before declaring UX done

- Can a first-time user complete the primary task without external help?
- Have you designed loading, empty, partial, full, error, and success states?
- Are destructive actions confirmed or undoable?
- Does the copy read as if a person wrote it?
- Does the page have a single, obvious primary action?
- Can a keyboard-only user complete the task?
- Have you removed every element that does not serve a task?
