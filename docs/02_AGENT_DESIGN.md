# AGENT_DESIGN: BizCopilot

## 🤖 The Hybrid Orchestrator
We use a **Hybrid Router-Specialist** design to balance speed and depth.

### 1. The Dispatcher (Router)
- **Purpose:** Analyzes the prompt to minimize token usage and latency.
- **Logic:**
    - If prompt = simple retrieval → Send to **SQL Architect**.
    - If prompt = complex comparison/prediction → Send to **Python Analyst**.
    - If prompt = unclear → Ask clarifying question.

### 2. SQL Architect (The Retriever)
- **Input:** NL Query + Schema Context (from RAG).
- **Output:** Valid, optimized PostgreSQL query.
- **Self-Correction:** If SQL fails, the agent receives the error and tries one "self-heal" attempt.

### 3. Python Analyst (The Scientist)
- **Input:** NL Query + Raw Data Samples.
- **Output:** Python script using Pandas/Matplotlib/Scipy.
- **Constraint:** Code must be executed in a restricted environment.

### 4. Narrative Synthesizer (The Communicator)
- **Purpose:** Turns raw rows of data into a business story.
- **Output:** 
    - `summary`: A 2-3 sentence insight.
    - `viz_type`: The recommended chart (e.g., "line").
    - `viz_config`: JSON parameters for the frontend to render the chart.

## 🛠️ Tools Available to Agents
- `get_schema`: Returns table/column info.
- `execute_sql`: Runs query against Postgres.
- `run_analysis`: Executes Python code in sandbox.
- `search_docs`: Queries internal documentation/KPI definitions.
