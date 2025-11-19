# Prompt: The "Empathetic" Pair Programmer

**Goal:** A VS Code extension that uses Multimodal Sensing (Audio + Screen + Typing Cadence) to detect developer frustration and intervene with context-aware, empathetic help.

**Prompt:**
> "Design the comprehensive architecture and key implementation details for a VS Code Extension called 'PairDev'.
>
> **Core Concept:**
> An AI that doesn't just read your code, but reads *you*. It detects 'Coding Rage' or 'Stuck States' and intervenes before you burn out.
>
> **1. Sensory Input System (Client-Side):**
> *   **Audio Listener:** Use Web Audio API to detect acoustic signatures of frustration (sighing, fast/heavy typing, groans). *Privacy Note:* Local processing only; do not stream raw audio. Trigger on decibel spikes or specific spectral patterns.
> *   **IDE Telemetry:** Listen to `vscode.workspace.onDidChangeTextDocument`.
>     *   Metric: `deletion_rate` (Are they deleting code as fast as they write it?).
>     *   Metric: `error_density` (Is the 'Problems' tab filling up?).
>     *   Metric: `tab_switching_velocity` (Frantic switching often implies confusion).
>
> **2. The 'Frustration Snapshot' (The Prompt):**
> When the 'Frustration Index' crosses a threshold (e.g., 75/100):
> *   Bundle the current file content, the last 5 terminal error messages, and the git diff.
> *   **Prompt Gemini 3:** 'The user is frustrated. Analyze this context. Identify the *single* most annoying blocker right now. Is it a syntax error, a logic bug, or an environment issue? Be concise and empathetic.'
>
> **3. The Intervention UI:**
> *   **Subtle:** Do NOT use a modal alert.
> *   **Status Bar:** Change color (e.g., from Blue to Amber).
> *   **Action:** If the user clicks the status bar, open a Webview Panel.
> *   **Content:** Display a 'Solution Card' offering a fix, but also a 'Break Suggestion' (e.g., 'You've been fighting this generic type error for 20 minutes. Want to try this syntax, or grab a coffee?').
>
> **Deliverables:**
> *   `extension.ts`: Main activation logic and event listeners.
> *   `frustrationDetector.ts`: The heuristic logic for calculating the stress score.
> *   `geminiClient.ts`: The interface for sending the snapshot."
