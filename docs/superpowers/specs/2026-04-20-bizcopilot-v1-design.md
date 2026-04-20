# BizCopilot V1: NL-to-Insights Design (Option B)

**Date:** 2026-04-20
**Status:** Approved (Architecture & Infrastructure)
**Goal:** Implement a production-grade Natural Language to SQL/Analytics pipeline for existing PostgreSQL databases.

---

## 🏗️ System Architecture

BizCopilot V1 is designed as a **Cloud-Native Mirror**, using Docker Compose to local-host services that will eventually run on Google Cloud Platform.

### 🧩 Components

1.  **Orchestrator (Backend):**
    *   **Framework:** FastAPI.
    *   **Agent Engine:** **Google ADK (Agent Development Kit)**.
    *   **LLM:** `gemini-2.5-pro` (via Vertex AI / Gemini API).
    *   **Role:** Intent routing, SQL generation, and analytical reasoning coordination.

2.  **Knowledge Base (Vector Store):**
    *   **Engine:** **Weaviate** (Standalone Docker Container).
    *   **Usage:** Stores semantic embeddings of the target PostgreSQL schema to provide high-precision RAG context for the Agent.

3.  **Data Persistence (Existing DB):**
    *   **Engine:** PostgreSQL (Local instance via PGAdmin4).
    *   **Access:** Connected via `host.docker.internal` or direct network bridge.

4.  **Analytics Engine:**
    *   **Environment:** Restricted Python sandbox for executing analytical code (Pandas, Scipy).
    *   **Integration:** Triggered by Google ADK for non-SQL reasoning tasks.

---

## 🔄 Data Flow (V1)

1.  **Ingestion:** The system introspects the existing PostgreSQL database schema.
2.  **Indexing:** Schema metadata (table names, column descriptions, relationships) is embedded and stored in Weaviate.
3.  **Query Loop:**
    *   User asks: "What was the total revenue per product category last month?"
    *   **ADK Coordinator** retrieves relevant table metadata from Weaviate.
    *   **SQL Architect** generates PostgreSQL query using `gemini-2.5-pro`.
    *   **Verification Agent** audits the SQL for security and correctness.
    *   **Executor** runs query against the existing PostgreSQL DB.
    *   **Synthesizer** formats the result into a human-readable insight.

---

## 🛠️ Infrastructure (Option B)

### `docker-compose.yml` (Target)
*   `bizcopilot-backend`: FastAPI + Google ADK logic.
*   `bizcopilot-weaviate`: Standalone Vector DB.
*   `bizcopilot-worker`: Isolated Python execution environment.

### 🔐 Security & Constraints
*   **Credentials:** All secrets (DB password: `@HillPatel07`, API keys) stored in `.env`.
*   **Sanitization:** SQL Architect must use READ-ONLY connections and exclude sensitive schemas.

---

## ✅ Success Criteria
- 90%+ accuracy on standard business queries (Aggregations, Joins, Time-series).
- Sub-5 second end-to-end response time.
- Successful introspection and indexing of any user-provided PostgreSQL schema.
