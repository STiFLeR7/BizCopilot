# DEVELOPMENT_PHASES: BizCopilot

## 🏁 Phase 1: Foundation (Weeks 1-2)
- **Repo Setup:** Monorepo structure, Docker configuration.
- **Database:** PostgreSQL setup, Alembic initialization, `user_data` schema logic.
- **API:** FastAPI boilerplate, Auth (JWT), File upload endpoint.
- **Data Ingestion:** CSV to Postgres pipeline with type inference.

## 🧠 Phase 2: AI Engine (Weeks 3-4)
- **RAG Implementation:** FAISS/Weaviate setup, schema embedding logic.
- **Orchestration:** LangGraph router and SQL Architect implementation.
- **SQL Verification:** Linter/Dry-run tool for generated SQL.
- **Basic Chat:** Backend-only chat sessions with persistent history.

## 📊 Phase 3: Analytics & Viz (Weeks 5-6)
- **Python Sandbox:** Secure execution environment for Pandas.
- **Python Analyst Agent:** Implementation of the Analysis path in LangGraph.
- **Visualization:** JSON spec for Recharts/Compose charts.
- **Mobile Integration:** Android app connection to API, basic chat UI.

## 🚀 Phase 4: Polish & Scale (Weeks 7-8)
- **Caching:** Redis implementation for query results.
- **Refinement:** Prompt engineering for 85%+ accuracy.
- **UI/UX:** Web dashboard, Android dashboard, interactive charts.
- **Deployment:** Render (Backend) and Vercel (Frontend) production setup.
