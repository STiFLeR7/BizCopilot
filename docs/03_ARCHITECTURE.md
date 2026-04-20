# ARCHITECTURE: BizCopilot

## 📐 System Overview
BizCopilot V1 uses a **Cloud-Native Mirror** architecture. It leverages Docker Compose to host services locally that are architecturally aligned with Google Cloud Platform (GCP).

## 🧩 Logical Components

### 1. Backend (FastAPI + Google ADK)
- **Orchestrator:** Coordinates agents using **Google ADK**.
- **LLM:** Powered by `gemini-2.5-pro`.
- **Identity:** Manages user sessions and connection strings to existing DBs.

### 2. Knowledge Base (Weaviate)
- **Vector Store:** Standalone **Weaviate** instance.
- **RAG:** Stores embedded schema metadata to provide high-precision context to the SQL Architect.

### 3. Data Layer (Existing PostgreSQL)
- **Engine:** Connects to the user's existing PostgreSQL instance (via local bridge or PGAdmin4).
- **Execution:** Runs audited SQL queries against the target schema.

### 4. Analytics Engine (Worker)
- **Python Sandbox:** Isolated environment for executing analytical code (Pandas, Scipy) triggered by Google ADK.

### 5. Client Layer
- **Web App:** Dashboard view + Chat interface (Deployed on GCP/Docker).
- **Android App:** Native chat interface + real-time dashboards.

## 🔄 High-Level Data Flow
1. **Ingestion:** System introspects existing PostgreSQL schema and indexes metadata into **Weaviate**.
2. **Query:** User sends NL query via Android/Web.
3. **Reasoning:** **ADK Coordinator** retrieves schema context from Weaviate.
4. **Generation:** **SQL Architect** generates PostgreSQL query using `gemini-2.5-pro`.
5. **Audit:** **Verification Agent** checks SQL for security and correctness.
6. **Execution:** Query runs against the existing DB; results fetched.
7. **Synthesis:** **Synthesizer** creates text summary + Chart JSON spec.
8. **Output:** Client renders insight + interactive chart.
