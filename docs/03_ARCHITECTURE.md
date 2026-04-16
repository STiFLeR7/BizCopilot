# ARCHITECTURE: BizCopilot

## 📐 System Overview
BizCopilot uses a **Modular Monolith** architecture. The core logic is centralized in the FastAPI backend, which orchestrates specialized agents and data execution environments.

## 🧩 Logical Components

### 1. API Gateway (FastAPI)
- Handles Request/Response lifecycle.
- Manages file uploads (CSV/XLSX).
- Handles user authentication and JWT sessions.

### 2. The AI Orchestrator (LangGraph)
Acts as the "Brain" of the system using a **Hybrid Router** pattern:
- **Router:** Classifies the prompt (e.g., "Show me sales" vs. "Why did sales drop?").
- **SQL Architect:** Generates PostgreSQL queries for data retrieval.
- **Python Analyst:** Generates code for deeper statistical analysis.
- **Narrative Synth:** Combines raw data + analysis into a human-readable summary.

### 3. Data Execution Layer
- **PostgreSQL Engine:** Executes generated SQL against dynamic user schemas.
- **Python Sandbox:** An isolated environment to run analysis code (Pandas, Numpy) without risk to the host system.

### 4. Client Layer
- **Web App:** Dashboard view + Chat interface.
- **Android App:** Native chat interface + push notifications for insights.

## 🔄 High-Level Data Flow
1. **Input:** User sends NL query via Android/Web.
2. **Context:** System retrieves table schemas from Vector DB (RAG).
3. **Plan:** Router decides: SQL retrieval, Python analysis, or both.
4. **Execute:** Queries run against Postgres; results fetched.
5. **Format:** Narrative Synth creates text summary + Chart JSON spec.
6. **Output:** Client renders message + interactive chart.
