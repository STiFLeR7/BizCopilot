# 01_TECH_STACK: BizCopilot

## 🏗️ Core Infrastructure
- **Backend Framework:** FastAPI (Python 3.10+)
- **Database (Primary):** PostgreSQL 15+ (Application metadata + Dynamic user data)
- **Database (Vector):** FAISS or Weaviate (for Schema Context & RAG)
- **Cache & Memory:** Redis (Session state, rate limiting, and result caching)
- **Containerization:** Docker & Docker Compose

## 🧠 AI & Machine Learning
- **Orchestration:** LangGraph (Stateful multi-agent workflows)
- **LLM Providers:** OpenAI (GPT-4o/o1) or Anthropic (Claude 3.5 Sonnet)
- **Embeddings:** `text-embedding-3-small` (OpenAI)
- **Execution Sandbox:** Restricted Python environment (using `multiprocessing` or Docker-in-Docker)

## 🌐 Frontend (Web)
- **Framework:** React.js (Next.js 14 App Router)
- **Styling:** Vanilla CSS / Tailwind CSS (as per user preference, defaulting to Vanilla-like modular CSS)
- **Charts:** Recharts or D3.js
- **Deployment:** Vercel

## 📱 Mobile (Android)
- **Language:** Kotlin
- **Architecture:** MVVM (Model-View-ViewModel)
- **Networking:** Retrofit + OkHttp
- **UI:** Jetpack Compose (Modern, reactive UI)

## 🔄 DevOps & CI/CD
- **Hosting:** Render (Backend), Vercel (Frontend)
- **CI:** GitHub Actions
- **Logging:** Sentry / Loguru
