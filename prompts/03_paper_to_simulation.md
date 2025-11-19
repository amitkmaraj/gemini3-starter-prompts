# Prompt: Scientific Paper to Interactive Sandbox

**Goal:** Build an automated researcher agent that reads static PDF papers, extracts mathematical models, and generates interactive Python simulations to verify the claims.

**Prompt:**
> "Create a **Streamlit** application aimed at the academic and research community.
>
> **The Use Case:**
> Researchers spend hours deciphering static equations in PDFs. This tool instantly converts those equations into an interactive playground, allowing for 'What-If' analysis.
>
> **1. The Ingestion Pipeline:**
> *   Use `pypdf` or `unstructured` to extract text and LaTeX formulas from uploaded PDFs.
> *   **CRITICAL:** The prompt must explicitly ask Gemini 3 to *correct* any OCR errors in the formulas by inferring the mathematical context.
>
> **2. The 'Model Extraction' Agent (Gemini 3):**
> *   Task: Identify the core independent variables (inputs), dependent variables (outputs), and constants.
> *   Task: Translate the math into a clean, vectorized Python function using `numpy`.
> *   *Constraint:* The generated code must be self-contained and error-handled (checking for division by zero, etc.).
>
> **3. The UI Generator:**
> *   Dynamically generate a Streamlit script (`simulation_app.py`).
> *   For each input variable, map it to the appropriate UI widget:
>     *   Continuous range -> `st.slider`
>     *   Boolean switch -> `st.checkbox`
>     *   Categorical choice -> `st.selectbox`
> *   Graphing: Use `plotly.express` for interactive charts that update in real-time as sliders move.
>
> **4. The 'Peer Review' Sidebar:**
> *   In the generated app, include a sidebar where Gemini provides a critique:
>     *   'Assumption Check: The simulation assumes linear friction, but the paper suggests quadratic drag at high velocities.'
>
> **Deliverables:**
> *   `main.py`: The orchestrator app that takes the PDF and generates the sub-app.
> *   `extractor.py`: The prompt logic for math extraction.
> *   `template.py`: The Jinja2 template used to construct the final simulation file."
