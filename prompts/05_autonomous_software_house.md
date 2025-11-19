# Prompt: Autonomous Software House (The Multi-Agent Mesh)

**Goal:** Create a hierarchical, state-aware multi-agent system where a 'Product Manager' agent orchestrates specialized 'Developer' agents to build full-stack applications from a single sentence, ensuring consistency via a shared state contract.

**Prompt:**
> "Build a robust multi-agent framework using Python (leveraging `langgraph` or a custom class structure).
>
> **The Objective:**
> User says: 'Build a Kanban board for organizing family chores.'
> System produces: A fully coded React frontend + FastAPI backend, saved to disk, ready to run.
>
> **1. The Shared State (The 'Brain'):**
> Implement a `ProjectState` class (Pydantic model) that acts as the source of truth. It must store:
> *   `user_intent`: Original prompt.
> *   `architecture`: Selected stack (e.g., React/Vite + SQLite).
> *   `api_contract`: OpenAPI/Swagger JSON spec (crucial for preventing frontend/backend mismatch).
> *   `file_system`: A virtual map of filenames to content.
>
> **2. The Agent Roster:**
> *   **Agent A: The Architect (Deep Think Mode):**
>     *   Input: User intent.
>     *   Action: Design the `api_contract`. This is the binding document.
>     *   Output: Updates `ProjectState.api_contract`.
> *   **Agent B: The Backend Lead:**
>     *   Input: `api_contract`.
>     *   Action: Implement the server. *Must* strictly adhere to the defined routes and types.
> *   **Agent C: The Frontend Lead:**
>     *   Input: `api_contract`.
>     *   Action: Implement the UI. Uses the contract to generate a type-safe API client.
> *   **Agent D: The QA Engineer:**
>     *   Input: The generated code from B and C.
>     *   Action: Static analysis. Checks if the frontend imports match the backend exports. If not, it rejects the build and sends it back to B or C with specific error instructions.
>
> **3. Deliverables:**
> *   `orchestrator.py`: The main loop running the agents.
> *   `agents.py`: Class definitions for each persona, including their specific system prompts.
> *   `state.py`: The Pydantic models defining the shared memory.
> *   `run.py`: A script to launch the 'Software House'."
