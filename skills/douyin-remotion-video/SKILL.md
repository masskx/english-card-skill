---
name: douyin-remotion-video
description: Build Douyin/TikTok-style English vocabulary short videos using Remotion, Codex, and Alibaba DashScope CosyVoice TTS. Use only for English word-learning episodes such as word roots, prefixes, suffixes, related word groups, confusing words, pronunciation, meaning contrasts, and vocabulary memory cards with high-contrast black/yellow visuals, subtitle bars, and audio-driven timelines.
---

# Douyin Remotion Video

Use this skill when the user wants to turn English vocabulary material into a punchy Douyin-style word-learning short video, especially:

- A word root, prefix, suffix, word family, confusing word pair, or vocabulary list needs to become a short video.
- An English-learning Remotion project needs a black/yellow high-contrast vocabulary-card style.
- Alibaba Bailian/DashScope CosyVoice voiceover needs to drive subtitles and timing.
- Existing Remotion scenes need style, rhythm, subtitle, voice, or final-export review.

Do not use this skill for paper explanations, code-module explainers, architecture diagrams, general knowledge videos, or plug-and-play module projects. Those belong to separate skills or projects.

## Inputs

Typical inputs:

- Vocabulary content: target root/affix, word list, meanings, phonetics, example memory angle, or a brief idea for an English-learning episode.
- Episode brief: topic, audience, goal, platform, duration, key words.
- Data files: `src/data/words.ts`, `src/data/voiceScript.ts`, optional `src/data/subtitles.ts`.
- Existing Remotion project using React + TypeScript.
- Optional reference video or screenshot for English vocabulary visual style.

## Outputs

Expected outputs:

- A runnable English vocabulary Remotion episode.
- Data-driven vocabulary files.
- TTS segments in `public/audio/segments/`.
- Merged voiceover at `public/audio/main-voice.mp3`.
- Audio-derived timeline at `src/data/generatedVoiceTimeline.ts`.
- Final MP4, usually `out/root-word-template.mp4` or an episode-specific output path.

## Core Workflow

1. Read the vocabulary topic and write a short episode brief.
2. Convert the word-learning angle into a compact video script with a strong first-three-second hook.
3. Create or update data files, especially `voiceScript.ts` and vocabulary data such as `words.ts`.
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

- `src/data/voiceScript.ts`: canonical narration and subtitle source for the vocabulary episode.
- `src/data/generatedVoiceTimeline.ts`: generated from real audio durations.
- `src/timeline.ts`: derives scene timing from `generatedVoiceTimeline`.
- `src/utils/motion.ts`: shared motion helpers such as `slamIn`, `punchZoom`, `shake`, `flashOpacity`.
- `public/audio/main-voice.mp3`: only generated artifact Remotion should play with `<Audio>`.

## Safety Rules

- Never write API keys into source files, templates, examples, logs, or docs.
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
