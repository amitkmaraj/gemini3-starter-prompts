# Prompt: Multimodal AR Memory Palace

**Goal:** Create a spatial web application that uses video understanding to turn a physical room into an interactive 3D knowledge graph.

**Prompt:**
> "Build a high-fidelity prototype web application using **React**, **Three.js** (via `@react-three/fiber`), and **Gemini 3 Vision**.
>
> **The Vision:**
> Users capture a video of their environment. The AI 'scans' this environment, identifying stable physical surfaces and objects. Users can then 'pin' digital memories (notes, tasks, voice memos) to these physical objects, creating a spatially persistent 'Memory Palace'.
>
> **Architecture & Components:**
>
> 1.  **Frontend (React + Vite):**
>     *   **Video Uploader:** A drag-and-drop zone accepting `.mp4` or `.webm`.
>     *   **3D Viewport:** A canvas overlaying the video. Use `drei` for easy camera controls (`OrbitControls`).
>
> 2.  **The Gemini 3 'Spatial Reasoning' Prompt:**
>     *   *Input:* The video file.
>     *   *Instruction:* 'Analyze this video. Identify 5 distinct, stationary physical anchors (e.g., Lamp, Desk, Window). For each anchor, provide:
>         1.  A descriptive label.
>         2.  A bounding box or estimated normalized 2D coordinates (x, y) of its center.
>         3.  A suggested color code for a UI marker.'
>     *   *Output Format:* Strict JSON array.
>
> 3.  **The Association Engine:**
>     *   *Input:* User provides a text list of 5 items to remember (e.g., 'Buy milk', 'Call Mom', 'Project Deadline').
>     *   *Logic:* Use Gemini to semantically map items to objects.
>         *   *Example:* 'Call Mom' -> pinned to the 'Antique Phone' or 'Photo Frame'.
>         *   *Example:* 'Project Deadline' -> pinned to the 'Wall Clock'.
>
> 4.  **Interaction Design:**
>     *   Render interactive 3D spheres at the coordinates returned by Gemini.
>     *   On hover: The sphere glows.
>     *   On click: A `Html` overlay (from `@react-three/drei`) expands to reveal the memory and the AI's reasoning ('I attached this memory here because...').
>
> **Deliverables:**
> *   `App.jsx`: Main layout.
> *   `Scene.jsx`: The Three.js canvas setup.
> *   `GeminiService.js`: Handles the API call and JSON parsing logic.
> *   `styles.css`: Modern, dark-mode CSS."
