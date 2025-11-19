
**Role:** You are a Senior AI Engineer specializing in Google Cloud Architecture and the Google Agent Development Kit (ADK).

**Goal:** Architect and write the code for a distributed "Course Creator" multi-agent system.
**Constraint:** You **must** use the Google Agent Development Kit (ADK) patterns to define the agent logic.
**Architecture:** 4 Independent Microservices deployed on Google Cloud Run.

**The System Spec (A2A Architecture):**
Each agent is a standalone service (FastAPI) that wraps an ADK Agent. They communicate over HTTP.

  * **Orchestrator Agent:** Receives the user prompt. Its "tools" are actually HTTP clients that call the other 3 agents.
  * **Researcher Agent:** Uses ADK with a Search Tool (mocked or real).
  * **Judge Agent:** Uses ADK with an Evaluation Tool/Logic.
  * **Creator Agent:** Uses ADK to synthesize the final Markdown.

**Requirements:**

1.  **Directory Structure (Monorepo style):**

    ```text
    /course-creator-adk
      /shared_protocol   # Pydantic schemas for A2A communication
      /orchestrator      # ADK Agent + FastAPI wrapper
      /researcher        # ADK Agent + FastAPI wrapper
      /judge             # ADK Agent + FastAPI wrapper
      /creator           # ADK Agent + FastAPI wrapper
      docker-compose.yml # Local orchestration
    ```

2.  **The ADK Pattern:**
    For *each* service, create a class `AgentService` that utilizes the ADK:

      * Initialize the model (e.g., `gemini-2.5-pro`).
      * Define `tools`:
          * For the **Orchestrator**, define tools like `call_researcher_agent(topic)`, `call_judge_agent(content)`, etc.
          * For the **Researcher**, define a `web_search` tool.
      * Define `system_instruction`: A clear persona for that specific agent.

3.  **Communication Protocol (A2A):**

      * Use FastAPI to expose a `POST /process` endpoint.
      * The Orchestrator does not just run a linear script; it uses the LLM to decide *when* to call the Researcher or Judge based on the tool definitions.
      * Ensure the Dockerfiles are set up for Cloud Run (listening on `$PORT`).

**Deliverables:**

1.  **Shared Schemas:** Python code for the message envelope (Request/Response models).
2.  **The Orchestrator Code:** Show how to define an ADK Agent whose tools function as API clients to the other services.
3.  **The Worker Agents:** Show the code for the **Researcher** and **Judge** (showing how to wrap the ADK `generate_response` in a FastAPI route).
4.  **Infrastructure:** A `docker-compose.yml` file that simulates the Cloud Run URLs by networking the containers together.

-----

### Architecture Visual

This architecture ensures that your Orchestrator is the only one maintaining the high-level "State" of the course generation, while the workers are stateless functional units.

### Technical Note for You

Since you are using the ADK, the "Secret Sauce" here is how you define the **Orchestrator's tools**.

The Orchestrator shouldn't just say `requests.post(...)`. You want to wrap that request in a structured ADK tool definition:

```python
# Conceptual example for the Orchestrator's tool
def call_researcher(query: str) -> dict:
    """Useful for gathering information on a topic."""
    url = os.getenv("RESEARCHER_URL")
    response = requests.post(f"{url}/process", json={"input": query})
    return response.json()
```