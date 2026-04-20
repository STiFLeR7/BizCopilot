# AGENT_DESIGN: BizCopilot

## 🤖 Google ADK Orchestration
BizCopilot V1 uses **Google ADK (Agent Development Kit)** to coordinate multiple specialized agents in a "Cloud-Native Mirror" architecture.

### 1. ADK Coordinator (The Brain)
- **Purpose:** Intent routing and analytical reasoning coordination.
- **Logic:** Retrieves relevant table metadata from **Weaviate** and decides the execution path.
- **LLM:** `gemini-2.5-pro`.

### 2. SQL Architect (The Writer)
- **Input:** NL Query + Schema Context (from Weaviate).
- **Output:** Valid, optimized PostgreSQL query.
- **LLM:** `gemini-2.5-pro`.

### 3. Verification Agent (The Auditor)
- **Purpose:** Audits the generated SQL for security (read-only enforcement) and logical correctness.
- **Action:** Rejects or approves the query before execution.

### 4. Synthesizer (The Communicator)
- **Purpose:** Turns raw data results into human-readable business insights.
- **Output:** 
    - `summary`: A concise business insight.
    - `viz_type`: The recommended chart (e.g., "bar", "line").
    - `viz_config`: JSON parameters for frontend rendering.

## 🛠️ Tools Available to Agents
- `weaviate_search`: Retrieves schema metadata using semantic search.
- `execute_sql`: Runs query against the existing PostgreSQL DB.
- `python_sandbox`: Executes analytical code (Pandas, Scipy) triggered by Google ADK.
- `schema_introspection`: Reads current PostgreSQL metadata for indexing.
