# CRITICAL_CONSTRAINTS: BizCopilot

## 🛡️ Security & Safety
1. **SQL Injection & Safety:** All generated SQL must be audited by the **Verification Agent** and executed via **READ-ONLY** database connections.
2. **Sandbox Isolation:** Python execution (Pandas/Scipy) must happen in a restricted worker environment with NO network access and limited resource usage.
3. **Data Privacy:** Access is restricted to user-provided PostgreSQL schemas. Credentials must be stored securely in `.env` and never logged.

## ⚖️ Performance
1. **Latency:** Total end-to-end response time must be < 5 seconds.
2. **Database:** Successful introspection and indexing of schemas with up to 100 tables.
3. **Concurrent Queries:** System must handle at least 10 concurrent AI sessions per standard node.

## 📉 Reliability
1. **Hallucination Mitigation:** **Weaviate-based RAG** must provide precise schema metadata. SQL Architect must use `gemini-2.5-pro` with strict temperature settings.
2. **Verification:** Queries that fail the Verification Agent's security or logic audit must be blocked or sent for a single regeneration attempt.
3. **Fallback:** Graceful failure messages with rephrasing suggestions if the pipeline breaks.
