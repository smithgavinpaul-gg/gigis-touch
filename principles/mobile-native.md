# Mobile & Native

Synthesised from the mobile-oriented skills (`mobile-app-ui-design`, `awesome-skills/mobile-app-design`, `claude-android-skill`) and the platform conventions of iOS and Android.

Mobile is not "web on a small screen". It is a separate medium with distinct conventions, gestures, hardware affordances, and user contexts. Design that ignores the medium produces apps that feel like ports.

## Core positions

1. **Context defines the design.** Phones are used standing, walking, one-handed, in sunlight, in bed, in transit. Design for a user who has 30 seconds and one thumb, not a user at a desk.
2. **Respect platform conventions.** iOS users expect iOS patterns; Android users expect Android. Cross-platform designs that ignore both feel foreign on each. Differentiate where the brand earns it, conform where it doesn't.
3. **Touch is imprecise.** Fingers are blunt instruments. 44×44pt minimum targets, generous spacing, forgiving hit areas.
4. **Performance is design.** A 2-second perceived load on mobile is the difference between use and abandonment. Skeletons, optimistic UI, and offline-first behaviour are design decisions.
5. **The hardware is part of the system.** Safe areas, notches, dynamic islands, foldable hinges, haptic engines, accelerometers. Design with awareness of where the screen actually is.

## iOS conventions

- **Navigation**: bottom tab bar for primary destinations (3-5 items), navigation bar at top with title and back chevron. Modal sheets slide from below for transient flows. Push navigation for going deeper, modal for going sideways.
- **System fonts**: SF Pro Text, SF Pro Display, New York (serif). Dynamic Type respects the user's text-size setting.
- **System colours**: semantic system colours (label, secondaryLabel, systemBackground) auto-adapt to light and dark mode.
- **Controls**: native segmented controls, switches (not checkboxes for instant toggles), date pickers, the iOS keyboard with appropriate input modes.
- **Gestures**: swipe-from-left-edge to go back, swipe-down on modal sheets to dismiss, swipe on table rows for actions.
- **Haptics**: light, medium, heavy impact feedback for actions, success/warning/error notifications for results.
- **Safe areas**: respect the notch, home indicator, and dynamic island. SwiftUI handles this automatically; in React Native / Expo, use `react-native-safe-area-context`.

## Android conventions (Material Design)

- **Navigation**: bottom navigation bar (3-5 items) or navigation drawer. Floating action button (FAB) for the primary action on a screen. App bar at top.
- **System fonts**: Roboto, with Roboto Flex as the modern variable counterpart.
- **Material colour system**: a dynamic colour scheme derived from a seed colour, with surface tonal elevation (lighter = higher elevation).
- **Controls**: switches for instant toggles, checkboxes for confirmable selections, Material 3 components.
- **Gestures**: back gesture from either edge, predictive back (Android 13+), swipe-to-refresh.
- **Ripple effects**: every tappable surface should ripple on press. Material's signature feedback.
- **Edge-to-edge**: content extends behind status bar and navigation bar, with inset-aware padding.

## When to break platform conventions

Brand-led apps (games, social apps, distinctive consumer apps) can and often should deviate. But deviate *deliberately*, with awareness of what you're losing:

- Custom tab bar instead of system tab bar → you lose system-level expectations (badge counts, accessibility behaviours) and must reimplement them.
- Custom typography instead of system fonts → you lose Dynamic Type / font-scale support unless you implement it yourself.
- Custom modals instead of system sheets → you lose swipe-down-to-dismiss and the OS's overlay management.

Brands like Instagram, Spotify, and Airbnb deviate consistently and earn it. Most apps should conform.

## Touch and gesture

- **Target size**: 44×44pt iOS / 48×48dp Android minimum. Spacing 8pt+ between targets.
- **Forgiving hit areas**: a 24pt icon button can have a 44pt tap target via padding.
- **Avoid hover.** Touch screens have no hover state. Don't design as if they do; that information must be visible by default.
- **Gestures should be discoverable.** Hidden gestures (long-press to reveal options, three-finger swipe) need education through onboarding or affordance hints.
- **Don't compete with system gestures.** A custom swipe-from-left-edge fights the iOS back gesture.

## Typography on mobile

- **Larger base size than web.** 17pt iOS body / 16sp Android body is the default, but consider 18pt+ for content apps.
- **Respect user font-size preferences.** Don't hard-code; use Dynamic Type / `font-size: medium` system tokens.
- **Tighten line-height slightly** vs desktop (1.3-1.4 for body), since mobile screens are scrolled more.
- **Avoid centred text** for any meaningful prose. Mobile scanning works best left-aligned.

## Layout for mobile

- **Single column** is the default. Multi-column rarely works under 600px.
- **Bottom-sheet-first**: actions that would be modal on desktop should be bottom sheets on mobile, reachable by thumb.
- **Pull-to-refresh** where data is fetched from a list.
- **Infinite scroll vs pagination**: infinite for content-discovery feeds, pagination for structured data (search results, transaction history).
- **Reachability**: primary actions in the bottom third of the screen, not the top. Thumbs live at the bottom.

## States on mobile

All the states from `principles/ux.md`, with mobile-specific notes:

- **Loading**: prefer optimistic updates over skeletons over spinners. The faster the app feels, the more it's used.
- **Empty**: a clear illustration or icon + one-line explanation + a primary action. Empty states do more work on mobile because they're more common (new user, no data, offline).
- **Offline**: a discrete banner ("You're offline. Some content may not be up to date.") and graceful degradation. Critical actions should queue and retry.
- **Error**: clear, actionable, and dismissable. Modal errors block flow; inline errors don't.

## Performance

- **Initial load matters most.** Lazy-load below-fold content, defer non-critical scripts, optimise images.
- **Image sizes**: serve appropriately-sized images, use WebP/AVIF, lazy-load.
- **Scroll performance**: 60fps minimum, 120fps where the device supports it. Avoid layout-thrashing scroll handlers.
- **Battery**: long-running JS, frequent network polls, and persistent location all drain. Design with awareness.

## Native vs cross-platform

- **Truly native (SwiftUI, Jetpack Compose)**: maximum platform fidelity, separate codebases. Best for apps where the platform-feel is core.
- **React Native / Expo**: shared code, near-native feel when used well, occasional escape hatches needed. Best for apps where time-to-market matters and UI is mostly conventional.
- **Flutter**: shared code, custom rendering engine, consistent across platforms but neither feels purely native. Best for branded apps that want consistent look.
- **PWA / web**: lowest fidelity but lowest cost. Best for content-first apps where install friction would lose users.

The choice is upstream of design but constrains it. Native components have native behaviour by default; cross-platform components must opt into platform behaviour.

## Accessibility on mobile

- **System text size**: support Dynamic Type / Android font-scale. Test at 200% scale.
- **VoiceOver / TalkBack**: every interactive element labelled.
- **Reduce Motion**: respect the system setting. Replace bouncy animations with crossfades.
- **High contrast / Smart Invert**: avoid hard-coded colours; use semantic tokens that adapt.
- **Touch accommodations**: tap accommodations (iOS) and switch access exist; don't break them.

## Hardware integrations

- **Camera, photos, location, microphone**: ask permission only when needed, with clear explanation. Pre-permission education screens (explaining why the app needs the permission *before* triggering the system dialog) significantly improve grant rates.
- **Push notifications**: ask permission contextually, not on app open. After the user has done something that would benefit from a notification.
- **Biometric auth (Face ID, Touch ID, fingerprint)**: as a convenience layer, not the only path. Always provide a passcode fallback.
- **Haptics**: small reinforcements (a light tap on selection), not constant rumbling.

## What to verify before declaring mobile design done

- Have you tested on a real device, not just a simulator?
- Have you tested in sunlight? In landscape? With one hand?
- Are touch targets 44×44pt minimum?
- Are primary actions reachable by thumb?
- Is safe-area padding handled (notch, home indicator)?
- Does the app behave reasonably offline?
- Does the app respect system text size and Reduce Motion?
- Are platform conventions followed where appropriate, deviated from deliberately where not?
- Does the app feel responsive at 60fps?
