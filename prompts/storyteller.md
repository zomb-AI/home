Create a complete production-ready single-file HTML app named "Storytellr".

Output requirement:
Return only one final `index.html` file with all HTML, CSS, and JavaScript embedded. Do not return explanations. Do not split into multiple files.

Product:
Storytellr is a bedtime story generator for parents. The parent fills in child-specific details, submits the form, OpenAI generates a personalized bedtime story, and the app immediately narrates that story using OpenAI TTS. The app must also support microphone input so the parent can speak an extra instruction, which is transcribed with OpenAI STT and inserted into the prompt.

Implementation reference:
Reuse the OpenAI browser-side interaction pattern from an existing CalorieGram `index.html`, but only the parts related to:
- microphone capture
- speech-to-text transcription
- OpenAI Responses API call
- text-to-speech playback
Do not include any meal, calorie, nutrition, history, or unrelated logic.

Core features:
- Single standalone HTML file
- Responsive layout for desktop and mobile
- Premium bedtime-themed visual design
- Settings modal for OpenAI API key and voice selection
- API key stored in localStorage
- selected TTS voice stored in localStorage
- clear loading, success, and error states
- automatic narration after story generation
- replay narration button
- stop narration button
- graceful fallback to browser `speechSynthesis` if OpenAI TTS fails

Form fields:
- Child first name (required)
- Child age in years (required)
- 2-3 things the child loves right now (required; at least one)
- Story theme or adventure type (optional; default to "adventure")
- Existing recurring characters (optional)
- Previous story / continuation context (optional)
- Time of night (optional select: early / regular / late)
- Story mode (optional select: standalone / continuation / extra calm)
- Extra parent instruction (optional textarea)

Voice note feature:
Add a microphone button labeled like "Hold to talk".
Behavior:
- on hold/touch, start browser microphone recording
- on release, stop recording
- send captured audio to OpenAI transcription API
- put returned transcript into the extra instruction textarea
- also show the transcript in the UI
- handle unsupported browsers and denied mic permission cleanly

OpenAI requirements:
Use browser `fetch()` calls directly to these APIs:
- transcription endpoint for STT
- Responses API for story generation
- speech endpoint for TTS

Story generation:
Use the Responses API to generate strict JSON output.

System prompt requirements:
The app must use a strong system instruction that enforces:
- the child is always the hero
- use the child’s real first name
- include at least one current love/favorite
- warm, soothing, safe bedtime tone
- no fear, no monsters, no danger to loved ones, no darkness-as-threat
- include a gentle age-appropriate challenge
- resolve through kindness, curiosity, or bravery
- end in a calm sleepy way back at bed, home, tent, sleeping bag, or safe resting place
- if scary story is requested, convert it into a gentle adventure instead
- if child is upset/restless, make the story extra cozy and calming
- calibrate length by age:
  - 3-4: 150-200 words
  - 5-6: 250-350 words
  - 7-8: 400-500 words
  - 9-10: 500-650 words

Construct the user prompt from form inputs clearly and explicitly.

Structured output schema:
Return strict JSON with:
- `title`
- `story_body`
- `character_notes`
- `continuation_hook`
- `spoken_story`

UI output:
Display:
- story title
- story body
- character notes
- continuation hook
- voice transcript/custom note area

Narration behavior:
After a successful LLM response:
- parse the JSON
- render the story in the UI
- immediately request OpenAI TTS for `spoken_story`
- auto-play the audio if possible
- if autoplay is blocked, prepare the audio and require a tap to replay
- include replay and stop controls
- if TTS fails, fall back to browser speech synthesis

Technical expectations:
- clean semantic HTML
- clean, readable JavaScript
- no frameworks required, but Tailwind CDN is allowed
- robust error handling
- mobile-friendly spacing and layout
- audio playback priming for Safari/iPhone-like restrictions
- use `localStorage` for API key and selected voice
- do not hardcode any secret
- do not use a backend
- do not use placeholder fake APIs

Important design direction:
Do not make it look generic. Give it a distinctive bedtime-story feel:
- elegant typography
- atmospheric night-sky or moonlit visual direction
- soft but rich colors
- polished cards, buttons, and states
- intentional spacing and hierarchy
- should feel like a real premium product, not a demo

Final constraint:
Return only the final complete HTML file and nothing else.
