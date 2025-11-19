# Prompt: The Dream Architect (Generative Storyboard)

**Goal:** A multimedia storytelling engine that converts abstract, chaotic dream descriptions into coherent, audio-visual cinematic trailers using a pipeline of text-to-script, text-to-image, and text-to-audio generation.

**Prompt:**
> "Create a Python-based content pipeline called 'DreamStream'.
>
> **The Input:**
> User records a voice note or types a ramble: 'I was running through a library, but the books were birds, and it was raining upside down...'
>
> **The Pipeline Steps:**
>
> **Step 1: The Narrative Structurer (Gemini 3 Text):**
> *   Turn the chaos into a structured screenplay format (sluglines, action lines, dialogue).
> *   Extract 5 Key Scenes.
>
> **Step 2: The Visual Director (Prompt Engineering):**
> *   For each Key Scene, generate a highly technical image prompt.
> *   *Requirements:* Specify camera lens (e.g., '35mm anamorphic'), lighting ('chiaroscuro'), and style ('surrealist oil painting').
> *   *Consistency:* Ensure the character description remains constant across prompts.
>
> **Step 3: Asset Generation:**
> *   Use a placeholder function `generate_image(prompt)` (mock this or connect to an API).
> *   Use a placeholder function `generate_music(mood)` to pick a soundtrack.
>
> **Step 4: The Editor (FFmpeg Automation):**
> *   Write a script that uses `ffmpeg` to:
>     *   Stitch the generated images together.
>     *   Apply a 'Ken Burns' effect (slow pan/zoom) to each static image to create movement.
>     *   Overlay the scene description text as subtitles.
>     *   Mix the background audio.
>
> **Deliverables:**
> *   `pipeline.py`: The linear execution flow.
> *   `script_generator.py`: Prompt logic for the screenplay.
> *   `ffmpeg_builder.py`: Python wrapper for generating the complex FFmpeg CLI command."
