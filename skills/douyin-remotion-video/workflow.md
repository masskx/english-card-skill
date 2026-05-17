# Workflow

## 1. Prepare The Episode

Create an episode brief from the source material.

Use `templates/episode_brief_template.md` and decide:

- Topic.
- Target viewer.
- Core promise.
- First-three-second hook.
- Key concepts.
- Final memory line.

For PDFs or code, extract only the strongest short-video idea. Do not attempt to explain everything.

## 2. Write Data Files

Create or update:

- `src/data/voiceScript.ts`
- Domain data such as `src/data/words.ts` or a new equivalent file.

Keep narration short and punchy. Use stable IDs:

- `hook`
- `flash-words`
- `same-root` or `pattern-reveal`
- `root-ject` or `core-concept`
- `word-*` / `concept-*`
- `grid-connect`
- `summary`
- `outro`

## 3. Build Or Adapt Remotion Scenes

Use data-driven components:

- Intro scene for hook and fast examples.
- Core concept reveal.
- One-by-one explanation scene.
- Structure/grid scene.
- Summary scene.
- Subtitle bar.

Use shared motion helpers in `src/utils/motion.ts`.

## 4. Generate Voice

Set the key in the current shell:

```powershell
$env:DASHSCOPE_API_KEY="your-key"
```

Run:

```powershell
npm run voice
```

Expected outputs:

- `public/audio/segments/001.mp3`
- `public/audio/main-voice.mp3`
- `src/data/generatedVoiceTimeline.ts`

If `instruction` fails, retry:

```powershell
$env:DASHSCOPE_TTS_USE_INSTRUCTION="false"
npm run voice
```

## 5. Sync Timing

`src/timeline.ts` should derive scene timing from `generatedVoiceTimeline`.

Rules:

- Current subtitle: active generated timeline segment.
- Current word or concept: active segment ID.
- Scene transitions: derived from segment IDs.
- Repeated flashing: based on progress through the active segment.

Avoid fixed second marks except as fallbacks.

## 6. Preview And QA

Run:

```powershell
npm run preview -- --port=3000
npx tsc --noEmit
```

Render stills around key beats:

```powershell
npx remotion still src/index.ts RootWordTemplate out/check-150.png --frame=150 --scale=0.5
```

Check `references/quality_rules.md`.

## 7. Export

Run:

```powershell
npm run render
```

Default output:

```text
out/root-word-template.mp4
```

## 8. Optimization Suggestions

Current flow works, but future episodes should improve:

- Shorten `voiceScript.ts` lines before TTS. Real TTS may be slower than expected.
- Keep `instruction` optional. Some DashScope voice/model combinations reject it.
- Consider a script mode that trims leading/trailing silence from each segment before measuring durations.
- Consider storing generated files under episode-specific names for batch production.
- Add an episode ID to output paths, such as `public/audio/<episode-id>/main-voice.mp3`.
- Add automated still checks for known beats to catch text overlap and stuck flash words.
- Keep a short "style lock" still frame reference for visual consistency between episodes.
