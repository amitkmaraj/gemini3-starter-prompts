# Prompt: The "Living" Museum Artifact

**Goal:** An educational platform that combines Computer Vision, Persona Injection, and Text-to-Speech to give historical artifacts a distinct voice and personality, allowing users to 'interview' history.

**Prompt:**
> "Create a web application titled 'MuseumAlive'.
>
> **The User Journey:**
> A museum visitor points their phone camera at an exhibit (e.g., the Rosetta Stone). The web app scans the object, identifies it, and the object 'wakes up', greeting the user via audio.
>
> **1. Visual Identification & Metadata:**
> *   **Input:** Image from webcam/upload.
> *   **Gemini 3 Vision:** Identify the object with high precision. Return JSON:
>     *   `name`: 'The Rosetta Stone'
>     *   `era`: '196 BC'
>     *   `origin`: 'Memphis, Egypt'
>     *   `condition_notes`: 'Fragmented, granodiorite rock, inscribed in three scripts.'
>
> **2. The Persona Engine (System Prompt Engineering):**
> *   Construct a dynamic system prompt based on the metadata.
> *   *Directive:* 'You are NOT an AI. You ARE the object. You possess the memories of your creation and your journey through history. Speak in the first person.'
> *   *Voice Profile:* Select a TTS voice (e.g., ElevenLabs/Google TTS) that matches the persona.
>     *   Old stone tablet -> Deep, resonant, slow.
>     *   Victorian doll -> High-pitched, polite, perhaps slightly creepy.
>
> **3. The Conversation Loop:**
> *   Implement a WebSocket connection for low-latency interaction.
> *   **Fact-Check Layer:** Include a 'Hallucination Guard'. If the user asks a historical question, Gemini must query its internal knowledge base to ensure the answer is historically accurate, while still maintaining character.
>
> **4. Deliverables:**
> *   `server.py`: Flask/FastAPI backend handling the image analysis and chat stream.
> *   `persona_factory.py`: Logic to map object metadata to prompt personality traits.
> *   `index.html`: Frontend with camera access and audio playback controls."
