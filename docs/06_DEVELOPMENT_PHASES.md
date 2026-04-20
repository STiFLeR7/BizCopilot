# DEVELOPMENT_PHASES: BizCopilot

## 🏁 Phase 1: Foundation & Ingestion (Weeks 1-2)
- **Repo Setup:** Docker-based "Cloud-Native Mirror" structure.
- **Database:** Local PostgreSQL setup and connection bridge (PGAdmin4).
- **Introspection:** Catalog crawling logic for existing database schemas.
- **API:** FastAPI boilerplate, Auth (JWT), and connection management.

## 🧠 Phase 2: Knowledge Base & RAG (Weeks 3-4)
- **Vector Store:** Standalone **Weaviate** implementation.
- **Indexing:** Embedding schema metadata using `gemini-2.5-pro`.
- **Orchestration:** **Google ADK** setup and basic intent routing.
- **Basic Chat:** Persistent chat sessions with schema-aware retrieval.

## 📊 Phase 3: SQL & Verification (Weeks 5-6)
- **SQL Architect:** Advanced prompt engineering with **gemini-2.5-pro**.
- **Verification:** Implementation of the **Verification Agent** for security/logic audits.
- **Analytics:** Integration of the Python sandbox worker for complex reasoning.
- **Visualization:** Development of the JSON spec for cross-platform charts.

## 🚀 Phase 4: Mobile & Cloud Scale (Weeks 7-8)
- **Mobile:** Android app integration (Chat + Real-time Dashboards).
- **Optimization:** Redis caching and fine-tuning query accuracy (Target: 90%+).
- **Cloud-Native Mirror:** Finalizing Docker Compose for **GCP** parity.
- **Deployment:** Production launch on GCP (Docker-based).
