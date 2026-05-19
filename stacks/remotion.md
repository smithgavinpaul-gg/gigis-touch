# Remotion

Synthesised from the Remotion-oriented skills (`remotion-superpowers`, `Claude-Code-Video-Toolkit`, `everything-claude-code`, `remotion-video-skill`, `claude-code-skills-lab`, `remotion-claude-video`) and the official Remotion Claude Code guide.

Remotion is React for video. The discipline below applies whether you're shipping product demos, social cuts, motion graphics, or full short-form video.

## Core positions

1. **Time is the canvas.** In Remotion, position is a function of frame. Every visual decision has a temporal counterpart: when does it appear, how long does it sit, when does it leave.
2. **Composition is structure.** A Remotion `<Composition>` is a self-contained piece. Most projects have one composition per deliverable; complex projects compose multiple compositions via `<Series>` or `<Sequence>`.
3. **Frames, not seconds, are the unit.** Reason in frames at the project's fps (30 / 60). Convert to seconds only at the boundaries (display, narration timing).
4. **Render is a deploy.** Once rendered, a Remotion piece is a video file. Build with the same care as production code: deterministic, reproducible, version-controlled inputs.
5. **Sound and motion together.** Audio cues drive motion; motion explains audio. Most weak Remotion work treats them separately.

## Project structure

A typical Remotion project:

```
src/
├── Root.tsx              # registers compositions
├── compositions/
│   ├── ProductDemo.tsx
│   ├── EventPromo.tsx
│   └── ArtistEpk.tsx
├── components/
│   ├── Title.tsx
│   ├── Lower.tsx          # lower-third
│   ├── Reveal.tsx
│   └── ...
├── assets/
│   ├── fonts/
│   ├── images/
│   └── audio/
└── styles/
    └── tokens.ts          # design tokens for the project
```

Keep compositions thin (composition is choreography); push visual logic into components.

## fps and dimensions

- **30fps** for narrative content where motion is mostly transitions and type reveals. Smaller file size, sufficient smoothness.
- **60fps** for motion-heavy or sport-like content where movement is the substance. Doubles render time and file size.
- **24fps** for cinematic feel. Strongly stylised.
- **Common dimensions**: 1920×1080 (16:9 horizontal), 1080×1920 (9:16 vertical for short-form), 1080×1080 (1:1 square), 1080×1350 (4:5 portrait for feeds).

Render multiple aspect ratios from one composition source where the budget allows; design the safe area for the most cropped format and let the wider formats breathe outwards.

## Timing and rhythm

- **Reason in frames.** A 2-second reveal at 30fps is 60 frames. Use `useCurrentFrame()` and `interpolate()` to drive animations.
- **Hold beats.** After a reveal, hold the result. Most weak work moves on too quickly. Display type wants 1.5-2 seconds visible at minimum.
- **Snap to music.** If the piece has music, identify the BPM and snap key moments to beats. A 120bpm track has a beat every 15 frames at 30fps (or every 0.5s).
- **Stagger entries.** Three lines of text entering simultaneously read as one event. Staggered by 4-8 frames each read as a sequence.

## `interpolate()` patterns

```tsx
import { useCurrentFrame, interpolate, Easing } from 'remotion';

const frame = useCurrentFrame();
const opacity = interpolate(frame, [0, 30], [0, 1], {
  extrapolateLeft: 'clamp',
  extrapolateRight: 'clamp',
  easing: Easing.out(Easing.cubic),
});
```

- Always clamp at both ends. Without it, values run unbounded and produce visual bugs.
- Choose easing per role: `Easing.out(Easing.cubic)` for entries, `Easing.in(Easing.cubic)` for exits, `Easing.bezier(0.16, 1, 0.3, 1)` for refined entrances.

## `spring()` for natural motion

```tsx
import { spring, useVideoConfig } from 'remotion';

const { fps } = useVideoConfig();
const scale = spring({
  frame,
  fps,
  config: { damping: 12, stiffness: 200, mass: 1 },
});
```

Springs are more natural than interpolations for entries. Tune damping (higher = less bouncy), stiffness (higher = faster), mass (higher = slower acceleration).

## Type in motion

(See `principles/typography.md` for the broader principles.)

- **Mask reveals over opacity fades.** Type clipped from below by a moving mask reads as deliberate; type fading in reads as a load state.
- **Stagger by word or line, not letter**, except for hero moments. Letter-by-letter is a strong effect; use once.
- **Hold long enough to read.** A 3-word headline needs at least 1.5 seconds visible. A sentence needs 3+ seconds.
- **Type weight should match the medium.** Video compresses; thin weights vanish on mobile playback. Lean heavier than you would on web (500-700 for body, 700-900 for display).

## Audio

- **Sync to audio**, not vice versa. Identify the music's structure (intro, drop, verse, build) and time visual events to it.
- **Use `<Audio>`** for music and SFX. Trim with `startFrom` and `endAt` props.
- **Voiceover timing**: line up subtitles or graphics to specific words. Use a transcript tool to get word-level timing, then snap visual events to those frames.
- **Sound design adds polish.** A whoosh on a reveal, a click on a card flip, an ambient pad under a slow section. Subtle SFX make low-budget video read as considered.

## Images and footage

- **`<Img>`** for static images. Pre-load to avoid render hiccups.
- **`<Video>`** for footage. Trim with `startFrom`, `endAt`. Mute (`muted`) when using separate audio.
- **Pre-process heavy assets.** Resize images to render dimensions before render; don't ship 4K source into a 1080p render.
- **Image overlays for branding.** A logo bug in the corner (with safe-area awareness) is more durable than burned-in chrome.

## Sequences and choreography

```tsx
<Series>
  <Series.Sequence durationInFrames={90}>
    <IntroBlock />
  </Series.Sequence>
  <Series.Sequence durationInFrames={120}>
    <MainBlock />
  </Series.Sequence>
  <Series.Sequence durationInFrames={60}>
    <OutroBlock />
  </Series.Sequence>
</Series>
```

`<Series>` plays sequences end-to-end. `<Sequence>` lets you offset a child by a fixed frame count for overlapping motion.

## Data-driven video

Remotion's strength is parameterised video. `getInputProps()` injects data into a composition at render time, so one composition produces many variations (per-customer, per-event, per-artist).

```tsx
import { getInputProps } from 'remotion';

const { name, date, venue } = getInputProps();
```

Use this for: personalised onboarding videos, event promos with per-event data, artist EPKs sourced from a CMS, sales reels with per-customer data.

## Render and deploy

- **Local render**: `npx remotion render` to a local file.
- **Remotion Lambda**: render at scale on AWS Lambda. Useful for variant explosion (e.g. 1000 personalised videos).
- **Output format**: H.264 mp4 for broad compatibility, ProRes / HEVC for higher quality, WebM / VP9 for web embeds.
- **Quality tuning**: `--codec`, `--crf`, `--pixel-format`, `--audio-bitrate`. Default settings are usually fine for social.

## Common anti-patterns

- **Linear easings everywhere.** Motion feels mechanical.
- **Too many simultaneous animations.** The eye can't track three things at once.
- **Type that flashes too fast to read.** A frequent mistake of dense motion graphics.
- **No audio.** Silent video reads as broken or unfinished, even when designed.
- **Logos that loiter.** A brand mark on screen the whole video reads as insecure. Use it at start, end, and one mid-point.
- **Auto-play with sound.** Most social platforms strip audio at thumbnail. Design for sound-off first, then add audio as a bonus layer.

## Optimisation

- **Preload assets** (`<Img>` and `<Video>`) to avoid stutter mid-render.
- **Concurrency**: Remotion renders in parallel by default. CPU-bound; not GPU-bound.
- **Composition functions should be pure.** Side effects in render functions cause non-determinism.
- **Memoise expensive calculations** with `useMemo` or `React.memo`.

## What to verify before declaring a Remotion piece done

- Have you played it at 0.5x speed and checked the easing feels right?
- Does every type element hold long enough to be read?
- Is the rhythm aligned to the music's beat structure?
- Does it read at sound-off (captions, visual events)?
- Have you tested all aspect ratios you're rendering?
- Does the file size fit the platform's upload constraint?
- Does the rendering deterministically produce the same file given the same input?
