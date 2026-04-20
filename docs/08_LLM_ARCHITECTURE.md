# LLM_ARCHITECTURE: BizCopilot

## 🏗️ The Multi-Stage Pipeline (Google ADK)

### Stage 1: Context Enrichment (RAG via Weaviate)
- **Task:** Retrieve high-precision schema snippets using semantic search.
- **Agent:** **ADK Coordinator** queries **Weaviate**.
- **Context:** Table descriptions, column types, and foreign key relationships.

### Stage 2: SQL Architecture (gemini-2.5-pro)
- **Task:** Generate production-grade PostgreSQL queries.
- **System Prompt:** "You are a Senior PostgreSQL Expert. Use READ-ONLY syntax. Adhere strictly to the provided Weaviate-retrieved schema."

### Stage 3: Verification (The Auditor)
- **Task:** Audit the generated SQL for security and logic.
- **Agent:** **Verification Agent** uses `gemini-2.5-pro` to check for:
    - Destructive commands (DROP, DELETE, UPDATE).
    - Efficient join logic and correct data types.

### Stage 4: Synthesis & Visualization
- **Task:** Transform raw data into business insights and JSON chart configs.
- **LLM:** `gemini-2.5-pro`.

## 🔄 Orchestration (Google ADK)
- **Agent Engine:** Uses **Google ADK** for intent routing and sub-task coordination.
- **Memory:** Context is maintained across turns to allow for follow-up questions (e.g., "Compare this to last year").
