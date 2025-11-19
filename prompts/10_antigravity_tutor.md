# Prompt: "Antigravity" Knowledge Gap Filler

**Goal:** A personalized, autonomous learning agent that builds a curriculum based on the 'Unknown Unknowns' in a user's reading history.

**Prompt:**
> "Design a background agent tailored for the 'Google Antigravity' ecosystem.
>
> **The Problem:**
> You read tech articles, but often skip over jargon. Over time, this creates a 'swiss cheese' knowledge base where you lack foundational concepts.
>
> **1. Input Source:**
> *   The agent accepts a list of URLs or text dumps (e.g., from a 'Read Later' app export).
> *   It also maintains a `user_profile.json`: `{'known_topics': ['Python', 'Basic SQL'], 'reading_level': 'Intermediate'}`.
>
> **2. The Gap Analysis Engine:**
> *   **Gemini 3 Task:** Scan the articles. Cross-reference mentioned concepts against the `user_profile`.
> *   Identify 'Gaps': Terms critical to the article's meaning that are likely outside the user's profile.
> *   *Filter:* Ignore trivial terms. Focus on high-value concepts (e.g., 'CRDTs', 'Paxos', 'Zero-Knowledge Proofs').
>
> **3. The Curriculum Builder (Spaced Repetition):**
> *   For each gap, generate a 'Micro-Lesson' card.
> *   **Format:**
>     *   **The Hook:** An analogy (e.g., 'Paxos is like a group of friends trying to agree on a pizza topping...').
>     *   **The Visual:** Generate a Mermaid.js flowchart syntax explaining the concept.
>     *   **The Code:** A tiny, pseudo-code implementation.
> *   **Schedule:** Implement a basic SM-2 (SuperMemo-2) algorithm to schedule *when* this lesson should be emailed to the user (Next review: 1 day, 3 days, 7 days).
>
> **4. Delivery Mechanism:**
> *   Generate a responsive HTML email template containing the day's lessons.
>
> **Deliverables:**
> *   `gap_detector.py`: The analysis logic.
> *   `scheduler.py`: The spaced repetition logic / database (SQLite).
> *   `teacher.py`: The content generation prompt."
