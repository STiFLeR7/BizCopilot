# 01_TECH_STACK: BizCopilot

## 🏗️ Core Infrastructure
- **Backend Framework:** FastAPI (Python 3.10+)
- **Database (Primary):** PostgreSQL 15+ (Local instance / PGAdmin4 connection)
- **Database (Vector):** **Weaviate** (Standalone Docker Container)
- **Cache & Memory:** Redis (Session state, rate limiting, and result caching)
- **Containerization:** Docker & Docker Compose

## 🧠 AI & Machine Learning
- **Orchestration:** **Google ADK (Agent Development Kit)**
- **LLM Providers:** **gemini-2.5-pro** (via Vertex AI / Gemini API)
- **Embeddings:** Google Vertex AI Embeddings
- **Execution Sandbox:** Restricted Python environment (for Pandas, Scipy execution)

## 🌐 Frontend (Web)
- **Framework:** React.js (Next.js 14 App Router)
- **Styling:** Vanilla CSS
- **Charts:** Recharts or D3.js
- **Deployment:** **GCP (Docker-based)**

## 📱 Mobile (Android)
- **Language:** Kotlin
- **Architecture:** MVVM (Model-View-ViewModel)
- **Networking:** Retrofit + OkHttp
- **UI:** Jetpack Compose (Modern, reactive UI)

## 🔄 DevOps & CI/CD
- **Hosting:** **GCP (Docker-based)** with "Cloud-Native Mirror" approach
- **CI:** GitHub Actions
- **Logging:** Google Cloud Logging / Sentry
