# Prompt: The "Deep Think" Heuristic Debugger

**Goal:** Build a production-grade CLI tool that leverages Gemini 3's "Deep Think" mode to solve impossible, non-deterministic bugs by performing a mental execution of code, git history, and logs simultaneously.

**Prompt:**
> "Act as a **Distinguished Engineer** at a FAANG company. Your task is to architect and implement a Python-based CLI tool called `deep-debug`.
>
> **The Core Philosophy:**
> Standard debuggers tell you *where* a crash happened. This tool tells you *why* the system drifted into a failure state, often finding bugs that traditional unit tests miss (e.g., race conditions, distributed system inconsistencies).
>
> **1. Technical Stack:**
> *   **CLI Framework:** `typer` (for clean, type-safe commands).
> *   **UI/UX:** `rich` (use `Console`, `Panel`, `Tree`, and `Live` for real-time feedback).
> *   **Git Integration:** `gitpython` to analyze commit history and diffs.
> *   **AI Client:** `google-genai` (targeting Gemini 3).
>
> **2. Input Schema:**
> The tool must accept a JSON configuration or CLI flags for:
> *   `--target`: Path to the specific module or directory to analyze.
> *   `--error-log`: Path to a raw stack trace or log file.
> *   `--context`: A natural language description of the symptom (e.g., 'Users report session loss after 20 minutes, but only on Tuesdays').
>
> **3. The 'Deep Think' Pipeline (Internal Monologue):**
> You must implement a workflow that forces the model to output a structured reasoning trace *before* the solution. The system prompt should enforce these steps:
> *   **Phase 1: Static Analysis:** Scan the code for dangerous patterns (e.g., unawaited async calls, mutable default arguments).
> *   **Phase 2: State Reconstruction:** Mentally 'replay' the execution flow described in the log. Track the state of critical variables at each step.
> *   **Phase 3: Hypothesis Generation:** Generate 3 competing theories for the bug. Disprove 2 of them using the evidence.
> *   **Phase 4: The Fix:** Generate the actual code correction.
>
> **4. Output Requirements:**
> *   **The Mental Trace:** Display a `rich.Tree` structure showing the model's deduction path.
>     *   *Example Node:* '⚠️ Suspicious lock acquisition in `DataManager.py:45`.'
>     *   *Example Child:* 'Analysis: Potential deadlock if `flush()` is called concurrently.'
> *   **Visual Proof:** Generate a Mermaid.js sequence diagram code block representing the *exact* sequence of events leading to the crash.
> *   **The Patch:** Provide a unified diff that can be directly applied.
>
> **5. Deliverables:**
> *   `debugger.py`: The main CLI entry point.
> *   `analyzer.py`: The logic for bundling code context and prompting Gemini.
> *   `prompts.py`: The rigorous system prompts used for the 'Deep Think' mode.
> *   `README.md`: Instructions on how to run it."
