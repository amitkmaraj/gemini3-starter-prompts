# Prompt: The Legacy Code "Archaeologist"

**Goal:** A code migration tool that focuses on "Cultural Translation" and "Historical Reasoning". It doesn't just translate syntax; it explains the *why* behind the original implementation.

**Prompt:**
> "Build a CLI tool specifically for modernizing legacy codebases (COBOL, Fortran, Java 6) into modern languages (Rust, Go, Python).
>
> **The Core Differentiation:**
> Standard transpilers result in 'Java-flavored Rust'—code that compiles but is unidiomatic. This tool acts as a 'Code Archaeologist', understanding that code is a product of its time.
>
> **1. Deep Reasoning Analysis (The Dig):**
> *   **Input:** A legacy file.
> *   **Gemini 3 Prompt:** 'Analyze this code. Identify patterns driven by hardware limitations of the era (e.g., manual memory management, loop unrolling for old CPUs, bit-packing). Explain the *intent*.'
>
> **2. The 'Cultural Debt' Report:**
> *   Before migrating, output a report flagging:
>     *   **Variable Naming:** 'Hungarian notation detected (e.g., `iCount`). Modern style recommends `count`.'
>     *   **Obsolete Patterns:** 'Singleton pattern used here to manage state; in Rust, we should use a module or ownership passing.'
>
> **3. The Migration (The Exhibit):**
> *   Generate the new code.
> *   **Feature:** Annotate the new code with `// ARCHAEOLOGIST NOTE:` comments.
>     *   *Example:* `// ARCHAEOLOGIST NOTE: The original code used a GOTO here to handle errors. We have replaced this with a localized Result<T, E> pattern for safety.`
>
> **4. Safety Verification:**
> *   If converting to Rust, the tool must attempt to run `cargo check` on the output. If it fails, feed the error back to Gemini for a self-correction loop (max 3 retries).
>
> **Deliverables:**
> *   `archaeologist.py`: CLI entry point.
> *   `translator.py`: Handles the prompt engineering and iterative repair loop.
> *   `history.py`: Generates the markdown report of the 'dig'."
