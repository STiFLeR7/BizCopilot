# 📄 Statement of Work (SoW)
Project: BizCopilot — Autonomous Business Analytics Copilot

## 1. 🧭 Project Overview
BizCopilot is an AI-powered business analytics platform that enables users to interact with their data using natural language. It combines GenAI, data pipelines, and analytics engines to deliver actionable insights, automated reports, and intelligent query execution.

The platform will support:
- Conversational analytics (chat-based querying)
- Automated data insights and summaries
- Dashboard visualization
- Cross-platform access (Web + Android)

## 2. 🎯 Objectives
- Build a production-grade AI-powered analytics assistant
- Enable non-technical users to query structured data easily
- Implement secure and scalable system architecture (Cloud-Native Mirror)
- Integrate real-time and batch analytics pipelines
- Deliver a multi-platform product (Web + Mobile)

## 3. 👥 Team & Responsibilities
- **Hill (Backend + AI/ML Lead)**
  - Design system architecture
  - Develop FastAPI backend services
  - Implement LLM pipelines (Google ADK, tool-calling, query generation)
  - Build Python execution sandbox for analytics
  - Integrate Weaviate vector database and embeddings
- **Yash (Android Frontend)**
  - Develop Android app (chat interface + dashboards)
  - API integration with backend
  - Implement real-time UI updates
- **Krish (Data Engineering)**
  - Manage existing PostgreSQL database connections
  - Design system metadata schema
  - Optimize query performance
- **Kushank (Data Analytics)**
  - Develop analytics logic and metrics
  - Build dashboards and visualizations
  - Generate business insights and reports

## 4. 🧩 Scope of Work
### ✅ Core Features (MVP / V1)
1. **Database Ingestion Layer**
   - Connect to existing PostgreSQL database (local/PGAdmin4)
   - Schema introspection and metadata extraction
2. **Conversational AI Engine (Google ADK)**
   - Natural language → SQL query generation using **gemini-2.5-pro**
   - Context-aware responses using Weaviate RAG
   - Multi-turn conversation support
3. **Analytics Execution Engine**
   - Python-based data analysis (sandboxed)
   - Query execution (PostgreSQL)
4. **Visualization Module**
   - Auto-generated charts (bar, line, pie)
   - Dashboard creation
5. **User Interface**
   - Web app (Vercel deployment)
   - Android app (chat + dashboards)

### 🚀 Advanced Features (V2+)
- Multimodal support (images/docs)
- Role-based access control (RBAC)
- Real-time streaming analytics
- Scheduled reports (daily/weekly insights)

## 5. 🏗️ System Architecture
- **Backend:**
  - FastAPI (API layer)
  - LLM orchestration (**Google ADK**)
  - Vector DB (**Weaviate**)
  - Redis (caching + session memory)
- **Data Layer:**
  - PostgreSQL (Primary target DB)
  - Dockerized analytics worker
- **Frontend:**
  - Web: React (Vercel)
  - Mobile: Android (Kotlin)
- **Deployment:**
  - Dockerized services (Cloud-Native Mirror)
  - Hosted on **GCP** (Production target)

## 6. 🔄 Workflow
1. User connects existing DB.
2. System introspects schema and indexes in Weaviate.
3. User asks query (natural language).
4. **Google ADK** converts → SQL / Python via **gemini-2.5-pro**.
5. Execution engine runs query against Postgres.
6. Results returned + visualized.

## 7. 📅 Timeline (Suggested – 8 Weeks)
- **Phase 1 (Week 1–2): Foundation**
  - Repo setup (monorepo + Docker Compose)
  - DB connectivity + Schema introspection logic
  - Weaviate setup & Indexing
- **Phase 2 (Week 3–4): Core Engine (ADK)**
  - Google ADK integration
  - gemini-2.5-pro prompt engineering
  - SQL Architect & Verification agents
- **Phase 3 (Week 5–6): Analytics + UI**
  - Python Sandbox & Visualization module
  - Android app integration
- **Phase 4 (Week 7–8): Scaling + Polish**
  - Caching (Redis)
  - Deployment (GCP / Vercel)
  - Testing + optimization

## 8. 📦 Deliverables
- Fully functional BizCopilot platform
- GitHub repository (production-ready structure)
- Android application (APK / build)
- Deployed backend & frontend
- Technical documentation

## 9. ⚠️ Risks & Mitigation
- **Incorrect SQL generation:** Multi-stage Verification layer (The Critic).
- **Data Security:** Read-only connections + sandboxed execution.
- **Performance:** Redis caching + Hybrid search optimization.

## 10. 📊 Success Criteria
- Accurate query-to-SQL conversion (>90%)
- Real-time response latency < 5 sec
- Successful ingestion of complex existing schemas
- Stable deployment mirroring GCP environment
