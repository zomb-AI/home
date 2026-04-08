# ZombAI-Caloriegram

Single-page voice meal tracker built in plain HTML, Tailwind CDN, and browser JavaScript. The app lets a user press and hold a mic orb, describe a meal, send audio to OpenAI for transcription and nutrition estimation, then hear back a natural-sounding spoken calorie and macro summary.

## What This App Does

- Records a spoken meal description with the browser microphone
- Sends audio to OpenAI Speech-to-Text
- Sends the transcript to OpenAI for calorie and macro estimation
- Speaks the result back using OpenAI TTS
- Shows the latest nutrition insight on screen
- Stores meal history locally in the browser
- Replays history cards with spoken nutrition summaries
- Uses a mobile-first voice UI with popovers, accordions, and animated playback states

## Files

- [index.html](/CalorieGram/index.html): complete application in a single file
- [README.md](/CalorieGram/README.md): product summary, setup notes, and the full build prompt

## OpenAI Key Instructions

This project is currently a browser-only prototype.

How the key works:

- The OpenAI API key is entered by the user inside the app `Settings` popover
- The key is stored in `localStorage` on that specific device/browser only
- The key is not shared automatically with other users opening the same hosted URL
- This is acceptable for personal demos and testing
- This is not recommended for a public production app

How to use the key:

1. Open the app.
2. Tap the `Settings` button in the top-right corner.
3. Paste your OpenAI API key into the `OpenAI API key` field.
4. Choose a playback voice if needed.
5. Tap `Save key`.
6. Press and hold the mic orb to start using the app.

Recommended note for anyone using this project:

- Each user should bring their own OpenAI API key
- If this app is made public, move OpenAI requests behind a backend proxy before wider sharing

## Hosting Notes

This app can be hosted as a static page on GitHub Pages.

That means:

- no local server is required after deployment
- microphone access works because GitHub Pages uses `https`
- `localStorage` continues to work for API key and history on each device

Important caveat:

- the app calls OpenAI directly from the browser
- for a real multi-user public product, use a backend so the OpenAI API key is never exposed client-side

## Full Build Prompt

Use the prompt below to recreate or regenerate this app in a single `index.html` file.

```text
Create a single-page mobile-first web app called "ZombAI-Caloriegram".

Output requirements:
- Return a complete standalone `index.html` file only
- Use plain HTML, inline CSS, inline JavaScript, Tailwind via CDN, Google Fonts, and Material Symbols
- Do not use React, build tools, bundlers, or external frameworks beyond CDN assets
- The entire app must work as a single static file

Branding:
- Product name: ZombAI-Caloriegram
- Header subtitle: Voice meal capture
- Use a circular badge with the letter "Z" instead of a profile photo
- Do not depend on external profile image URLs

Visual direction:
- Light theme only
- Use the existing bright nutrition palette style:
  - soft mint/green background
  - cyan accent for voice orb glow
  - emerald/green surfaces and labels
- Keep the experience polished, mobile-first, and premium
- Avoid generic spinner UI and avoid dark mode

Core experience:
- The main experience is voice-first
- The user presses and holds a large central mic orb to record
- On release, recording stops and analysis begins
- Audio goes to OpenAI STT
- Transcript goes to OpenAI for meal nutrition analysis
- Spoken response goes to OpenAI TTS
- The app then plays back calories and macro breakdown in a natural voice

Functional requirements:

1. Header
- Sticky top header
- Left: circular "Z" logo badge
- Title: ZombAI-Caloriegram
- Subtitle: Voice meal capture
- Right: settings button

2. Instruction card
- Compact card near the top
- Explain the flow briefly:
  - hold the orb
  - describe the meal
  - app transcribes, estimates, and speaks back the result
- Include:
  - API key status badge
  - Settings shortcut
  - Status text below
- On mobile, use smaller font sizes and tighter spacing

3. Transcript preview
- Small centered transcript/preview area above the mic orb
- Show transcript or placeholder guidance text

4. Mic orb section
- Large circular mic button centered on mobile
- Recording state:
  - pulsing orb
  - clear listening label
  - live red status dot
- Processing state:
  - keep mic icon stable
  - show a subtle rotating ring around the orb
  - show animated waveform/equalizer bars inside the orb
  - do not use a rotating arrow icon or generic spinner icon
- Pressing the mic while speech is already playing must stop the previous playback first

5. OpenAI integration
- Add a Settings popover where the user can:
  - paste an OpenAI API key
  - save it to localStorage
  - clear it
  - choose a TTS playback voice
- Store the API key in localStorage on that device only
- Add clear helper copy explaining this

6. Speech-to-text
- Use OpenAI `/v1/audio/transcriptions`
- Use `gpt-4o-mini-transcribe`
- Record using `MediaRecorder`
- Handle browser-supported mime types safely

7. Meal analysis
- Use OpenAI `/v1/responses`
- Ask for strict JSON schema output
- Required fields:
  - meal_name
  - transcript
  - total_calories
  - protein_g
  - carbs_g
  - fiber_g
  - fat_g
  - summary
- The system prompt should instruct the model to estimate nutrition from spoken meal descriptions and keep the summary practical

8. Spoken playback
- Use OpenAI `/v1/audio/speech`
- Use `gpt-4o-mini-tts`
- Voice should be selectable in Settings
- Speak a full nutrition sentence including:
  - meal name
  - calories
  - protein
  - carbs
  - fibre
  - fat
  - short summary
- If OpenAI TTS fails, fall back to browser speech synthesis
- If the analysis result indicates an unspecified meal, unknown meal, or no meal, do not speak anything

9. Last Insight section
- Add a section called "Voice Nutrition"
- Show:
  - Last Insight title
  - meal name
  - calorie card
  - protein card and bar
  - carbs card and bar
  - healthy fats card
  - spoken summary text block
- On mobile, this section must be collapsed by default
- Use an animated accordion open/close transition

10. History section
- Add a "History" accordion below the insight section
- On mobile, this section must also be collapsed by default
- Save recent meals in localStorage
- Show history cards with:
  - meal name
  - timestamp
  - calories
  - protein
  - carbs
  - fibre
  - fat
  - short summary
- Tapping a history card must:
  - stop any ongoing spoken audio
  - load the meal into Last Insight
  - show processing state briefly
  - replay the spoken nutrition summary if the meal is valid for speech

11. Playback insight popover
- As soon as TTS starts, open a blocking popover
- The popover must prevent access to the mic underneath until dismissed
- It should show:
  - meal title
  - calories
  - protein
  - carbs
  - fibre
  - fat
  - spoken summary
- User can dismiss at any time via close button or backdrop
- Use the same visual language as the main UI

12. Spoken highlight behavior inside popover
- Glow each nutrition card in spoken order:
  - calories
  - protein
  - carbs
  - fibre
  - fat
  - summary
- Keep the currently spoken card glowing longer
- Add a shimmer line moving across the active card
- Sync the summary paragraph line-by-line instead of only card-by-card
- Add a delayed start to the first glow so it aligns better with playback
- Clear all highlights when playback ends, is interrupted, or popover is dismissed

13. Scroll behavior
- When TTS starts, automatically scroll to the Last Insight section
- If the insight accordion is closed on mobile, open it first
- Home tab:
  - scroll the page all the way to the top
- History tab:
  - scroll the History section to the top just below the sticky header
  - then expand it with animation

14. Bottom navigation
- Bottom tab bar should contain only:
  - Home
  - History
- Remove Profile
- Remove bottom mic button
- Keep spacing balanced for the two-tab layout

15. State handling
- Stop current speech when:
  - user presses mic
  - user taps a history card
  - user starts a new playback flow
- Processing animation must start after recording ends and while OpenAI is working
- Processing animation must stop as soon as TTS begins
- Same processing behavior should apply when replaying from history

16. Accessibility and usability
- Use semantic buttons and labels
- Make controls touch-friendly
- Keep layout reliable on mobile devices
- Ensure accordions, popovers, and sticky header behave well on narrow screens

Implementation notes:
- Use localStorage keys for:
  - OpenAI API key
  - selected voice
  - meal history
- Create helper functions for:
  - saving/clearing key
  - recording UI
  - processing UI
  - transcription
  - meal analysis
  - speech playback
  - speech interruption
  - history rendering
  - accordion state
  - playback highlight sequence
- Include safe error handling and user-facing status messages
- Keep all logic in the same HTML file

OpenAI setup notes to surface in the app:
- Tell the user to open Settings and paste their OpenAI key
- Mention the key is stored only in this browser
- Mention each user should use their own key
- Mention browser-only storage is suitable for demo use, not public production security
```

## Suggested README Note For Users

If you are sharing this project link with someone else:

- they will not automatically receive your saved API key
- they will need to enter their own key on their own device
- their meal history will also be separate on their own browser

## Future Upgrade Path

If you want to make this production-ready later:

1. Move OpenAI calls to a small backend proxy.
2. Keep the frontend as a static deployment.
3. Store secrets in server-side environment variables.
4. Add authenticated user accounts if you want cross-device meal history.
