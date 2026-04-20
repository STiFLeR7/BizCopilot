# DATA_MODEL: BizCopilot

## 🗄️ Database Strategy

### 1. Application Database (PostgreSQL)
Stores application-level metadata and system state.
- `users`: Auth credentials, roles, and session settings.
- `connections`: Metadata for existing PostgreSQL databases (Host, Port, DB Name, encrypted credentials).
- `chat_sessions`: History of conversations for context retrieval.
- `query_logs`: Record of NL queries, generated SQL, execution status, and insights.

### 2. Knowledge Base (Weaviate)
Stores semantic representations of the connected database schemas to enable high-precision RAG.
- **Schema Objects:** Embedded metadata about tables, columns, and data types.
- **Relationship Map:** Indices of foreign key relationships and common join paths.
- **KPI Definitions:** Embedded business logic for standardized metrics.

### 3. Business Data (Target PostgreSQL)
The user's existing database instance (e.g., accessed via PGAdmin4).
- BizCopilot connects as a **READ-ONLY** user.
- Data remains in-place; only metadata is ingested for indexing.

## 🔄 Ingestion & Indexing Pipeline
1. **Connection:** User provides credentials for an existing PostgreSQL instance.
2. **Introspection:** System crawls the database catalog (`information_schema`) to map tables and columns.
3. **Embedding:** Metadata is processed by `gemini-2.5-pro` and stored in **Weaviate**.
4. **Maintenance:** Periodic re-syncing to detect schema changes (e.g., new tables/columns).
