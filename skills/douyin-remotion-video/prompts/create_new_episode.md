# Prompt: Create New Episode

Use the `douyin-remotion-video` skill.

Create a new Douyin-style Remotion short video episode from the source below. First extract the core idea, then write an episode brief, then implement the Remotion data/code changes.

Source:

`<paste idea, PDF path, code path, architecture diagram path, or notes>`

Requirements:

- Keep the black/yellow high-contrast style.
- Make the first three seconds urgent and clear.
- Use data-driven content.
- Write `src/data/voiceScript.ts`.
- Generate or update `src/data/generatedVoiceTimeline.ts`.
- Use voice timeline to drive current scene, subtitle, active keyword, and punch zoom.
- Do not hardcode API keys.
- Render key stills and final MP4.
