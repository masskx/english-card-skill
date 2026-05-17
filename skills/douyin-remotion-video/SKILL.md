---
name: douyin-remotion-video
description: Build Douyin/TikTok-style knowledge short videos from PDFs, code modules, architecture diagrams, or rough ideas using Remotion, Codex, and Alibaba DashScope CosyVoice TTS. Use when creating, adapting, voice-synthesizing, synchronizing, reviewing, or batch-producing high-contrast black/yellow Remotion explainer videos with subtitle bars and audio-driven timelines.
---

# Douyin Remotion Video

Use this skill when the user wants to turn source material into a punchy Douyin-style knowledge short video, especially:

- A paper PDF, report, code module, architecture diagram, or short idea needs to become a short video.
- A Remotion project needs a black/yellow high-contrast learning-video style.
- Alibaba Bailian/DashScope CosyVoice voiceover needs to drive subtitles and timing.
- Existing Remotion scenes need style, rhythm, subtitle, voice, or final-export review.

## Inputs

Typical inputs:

- Source content: PDF, notes, code snippets, diagrams, screenshots, or a brief idea.
- Episode brief: topic, audience, goal, platform, duration, key concepts.
- Data files: `src/data/words.ts`, `src/data/voiceScript.ts`, optional `src/data/subtitles.ts`.
- Existing Remotion project using React + TypeScript.
- Optional reference video or screenshot.

## Outputs

Expected outputs:

- A runnable Remotion episode.
- Data-driven content files.
- TTS segments in `public/audio/segments/`.
- Merged voiceover at `public/audio/main-voice.mp3`.
- Audio-derived timeline at `src/data/generatedVoiceTimeline.ts`.
- Final MP4, usually `out/root-word-template.mp4` or an episode-specific output path.

## Core Workflow

1. Read the episode source and write a short episode brief.
2. Convert the source into a compact video script with a strong first-three-second hook.
3. Create or update data files, especially `voiceScript.ts` and any domain data such as words, concepts, or steps.
4. Build Remotion scenes from data. Keep content, timing, and visual state separate.
5. Generate TTS voiceover with DashScope CosyVoice. Never hardcode the API key.
6. Use `ffprobe` durations to generate `generatedVoiceTimeline.ts`.
7. Drive subtitles, active scene, active keyword, and punch zoom from `generatedVoiceTimeline`.
8. Render still frames at key beats, inspect for overlap and poor contrast.
9. Render final MP4 and verify audio/video sync.

## Files To Load As Needed

- Visual style: `references/visual_rules.md`
- Timing and pacing: `references/rhythm_rules.md`
- DashScope voiceover: `references/voice_rules.md`
- Subtitle design and sync: `references/subtitle_rules.md`
- Export QA checklist: `references/quality_rules.md`
- End-to-end procedure: `workflow.md`
- Current example: `examples/ject_episode_example.md`

## Preferred Project Pattern

Keep these files data-driven:

- `src/data/voiceScript.ts`: canonical narration and subtitle source.
- `src/data/generatedVoiceTimeline.ts`: generated from real audio durations.
- `src/timeline.ts`: derives scene timing from `generatedVoiceTimeline`.
- `src/utils/motion.ts`: shared motion helpers such as `slamIn`, `punchZoom`, `shake`, `flashOpacity`.
- `public/audio/main-voice.mp3`: only generated artifact Remotion should play with `<Audio>`.

## Safety Rules

- Never write API keys into source, templates, examples, logs, or docs.
- Use `DASHSCOPE_API_KEY` from the environment.
- Treat generated audio and timelines as replaceable artifacts.
- Do not rely on hardcoded second marks once a generated voice timeline exists.
- If DashScope `instruction` fails for a system voice, retry without `instruction` while preserving `rate`, `voice`, `model`, and script structure.

## Useful Commands

```powershell
npm run voice
npm run preview -- --port=3000
npm run render
npx tsc --noEmit
```

For keyframe checks:

```powershell
npx remotion still src/index.ts RootWordTemplate out/check.png --frame=150 --scale=0.5
```
