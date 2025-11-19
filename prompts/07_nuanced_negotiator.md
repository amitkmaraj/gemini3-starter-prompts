# Prompt: The Nuanced Negotiator (EQ Trainer)

**Goal:** A text-based roleplay simulator that analyzes the user's 'Emotional Intelligence' (EQ), subtext, and negotiation tactics in real-time, providing a 'Shadow Analysis' of the conversation.

**Prompt:**
> "Develop a sophisticated Python terminal application for leadership and negotiation training.
>
> **The Scenario:**
> The user plays a Tenant negotiating rent with a Landlord (the AI).
>
> **1. The Dual-Model Architecture:**
> You must implement an `async` loop that triggers two distinct Gemini 3 calls for every user message:
> *   **The Actor (The Landlord):** Responds to the user. Has a hidden 'Patience Meter' (0-100). If it hits 0, they walk away.
> *   **The Shadow (The Coach):** Silent observer. Analyzes the user's message for:
>     *   *Valence/Arousal:* Is the user angry, calm, passive-aggressive?
>     *   *Tactics:* Did they use 'Anchoring', 'Mirroring', or 'Ultimatums'?
>     *   *Subtext:* What did they *really* mean?
>
> **2. The Feedback UI:**
> *   Use `textual` or `rich` to create a split-screen layout.
> *   **Left Panel:** The Chat (User vs. Landlord).
> *   **Right Panel:** The 'Live EQ Dashboard'.
>     *   Update a progress bar for 'Rapport'.
>     *   Display 'Analyst Notes': '⚠️ User used an ultimatum too early. Landlord patience dropped by 15%.'
>
> **3. The 'Replay' Feature:**
> *   At any point, allow the user to type `/fork`.
> *   The tool should branch the conversation from the current point, allowing the user to try a different approach to see how the outcome changes (e.g., 'What if I had been nicer here?').
>
> **Deliverables:**
> *   `negotiator.py`: Main event loop.
> *   `analysis_engine.py`: The prompts for the 'Shadow' observer.
> *   `scenarios.json`: Configuration file defining different roleplay setups (Salary Negotiation, Used Car Sale, Breakup)."
