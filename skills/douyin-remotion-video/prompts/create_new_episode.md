# Prompt: Create New Episode

Use the `douyin-remotion-video` skill.

Create a new Douyin-style English vocabulary Remotion short video episode from the word-learning topic below. First extract the memory angle, then write an episode brief, then implement the Remotion data/code changes.

Source:

`<paste word root, prefix, suffix, word list, confusing words, pronunciation topic, or notes>`

Requirements:

- Keep the black/yellow high-contrast style.
- Make the first three seconds urgent and clear.
- Use data-driven vocabulary content.
- Write or update `src/data/words.ts`.
- Write `src/data/voiceScript.ts`.
- Generate or update `src/data/generatedVoiceTimeline.ts`.
- Use voice timeline to drive current scene, subtitle, active keyword, and punch zoom.
- Do not hardcode API keys.
- Render key stills and final MP4.
