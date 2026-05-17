# Quality Rules

Use this checklist before delivering an episode.

## Content

- The first three seconds have a clear hook.
- The viewer knows why the topic matters.
- Each line teaches one idea.
- No line sounds like textbook narration unless intentionally academic.
- The final summary is memorable.

## Visual

- Black/yellow theme is consistent.
- Current keyword dominates the screen.
- Supporting text does not compete with the main word.
- No text overlaps or gets clipped.
- Subtitles fit inside the bottom bar.
- Grid/diagram lines do not cover important text.
- Background texture is subtle enough for readability.

## Rhythm

- Visual changes happen every 1-2 seconds.
- Flash-word sequences are tied to segment progress, not hardcoded frame slots.
- Current word punch zoom occurs at the start of each word segment.
- Scene changes align with generated voice timeline.
- The final hold is long enough for editing.

## Voice

- `public/audio/main-voice.mp3` exists.
- `public/audio/segments/*.mp3` exist.
- `generatedVoiceTimeline.ts` was regenerated after the latest voice run.
- Audio does not include the instruction text.
- English keywords are understandable.
- Narration is not too slow for Douyin style.

## Technical

- `npx tsc --noEmit` passes.
- Key still frames render.
- Full `npm run render` completes.
- The final MP4 plays with audio.
- No API key is in committed files.
- Generated files are intentionally included or ignored according to the project policy.

## Suggested Still Frames

Render frames around:

- Hook: 0.4s.
- Flash words: several points across the segment.
- Root reveal.
- First word explanation.
- Mid word explanation.
- Grid scene.
- Final summary.

Example:

```powershell
npx remotion still src/index.ts RootWordTemplate out/check.png --frame=150 --scale=0.5
```
