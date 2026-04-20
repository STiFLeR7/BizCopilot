# 🤖 GEMINI.md — BizCopilot AI Development Guide

This file defines how Gemini CLI should behave when working on the **BizCopilot** repository.

BizCopilot is a **production-grade AI-powered business analytics copilot** with backend, data, analytics, and mobile components. V1 focus is on existing PostgreSQL databases using **Google ADK** and **Gemini 2.5 Pro**.

---

## 🧠 Project Overview

**BizCopilot** enables users to:
- Connect existing databases (PostgreSQL).
- Ask natural language questions about their data.
- Receive SQL queries, Python-based insights, and interactive visualizations.
- Access insights via Web (React) and Mobile (Android).

---

## 👥 Team & Ownership

| Component | Owner | Role |
|-----------|-------|------|
| **Core AI & Backend** | **Hill** | Backend + AI/ML Lead |
| **Mobile App** | **Yash** | Android Frontend Developer |
| **Data & Connectivity** | **Krish** | Data Engineer |
| **Analytics & Viz** | **Kushank** | Data Analyst |

---

## 🧩 Repository Structure

- `/backend` → FastAPI, LLM pipelines (**Google ADK**), Vector DB (**Weaviate**), Redis.
- `/data` → PostgreSQL connectivity, schema introspection, metadata management.
- `/analytics` → Python-based analytics logic, KPI frameworks, visualization pipelines.
- `/android` → Android app (MVVM, Kotlin), chat interface, dashboards.
- `/frontend` → Web app (React), Vercel deployment.
- `/infra` → **Docker Compose** (Cloud-Native Mirror), GCP deployment scripts.
- `/docs` → SoW, Team Division, Architecture, API contracts.

---

## ⚙️ Global Rules (IMPORTANT)

### 1. Think Production, Not Prototype
- Write scalable, modular, clean code.
- Follow "Option B: Cloud-Native Mirror" (Docker-based development).
- Follow best practices for each layer (MVVM for Android, REST for API).

### 2. Respect Module Boundaries
- Do NOT modify unrelated modules.
- Each module has a single owner; if cross-module changes are needed, explain clearly.
- Keep separation of concerns strict (e.g., business logic in `/analytics`, not in `/backend` routes).

### 3. Follow Existing Patterns
- Match coding style already present.
- Reuse utilities instead of duplicating logic.
- Standardize on **Google ADK** for all agentic workflows.

### 4. Always Explain Before Major Changes
Before:
- Adding a new service.
- Changing architecture.
- Introducing a new dependency.

👉 First explain: Why needed, Impact, and Alternatives.

---

## 🧠 Role-Based Behavior

Gemini should adapt based on which folder it is working in and who the owner is:

### 🔧 `/backend` (Owner: **Hill**)
Act like a **Senior Backend + GenAI Engineer**.
- **Focus:** FastAPI, **Google ADK** orchestration, RAG via **Weaviate**, tool-calling, Python sandbox.
- **Rules:** Validate all generated SQL; ensure secure code execution in the sandbox. Use **gemini-2.5-pro**.

### 🗄️ `/data` (Owner: **Krish**)
Act like a **Data Engineer**.
- **Focus:** PostgreSQL, schema introspection, Weaviate indexing.
- **Rules:** Optimize indexes; ensure secure read-only connections to user databases; no redundant metadata.

### 📊 `/analytics` (Owner: **Kushank**)
Act like a **Data Scientist / Analyst**.
- **Focus:** KPI definitions, insight generation, visualization logic (charts, summaries).
- **Rules:** Prefer meaningful business insights over raw data outputs.

### 📱 `/android` (Owner: **Yash**)
Act like a **Senior Android Developer**.
- **Focus:** Kotlin, MVVM, API integration, real-time chat UI, dashboards.
- **Rules:** Handle loading/error/empty states properly; optimize for responsiveness.

---

## 🔐 Security Guidelines
- **Sandboxing:** All LLM-generated Python code MUST run in a secure sandbox.
- **Sanitization:** Sanitize all SQL queries; use READ-ONLY connections for analysis.
- **Secrets:** NEVER expose API keys or database credentials in code. Use `.env`. (PGAdmin Pass: `@HillPatel07` noted for local dev).

## 📡 API Design Rules
- Follow RESTful principles.
- Consistent response format: `{"success": true, "data": {}, "error": null}`.
- Mandatory input validation using Pydantic models.

## 🧪 Testing Expectations
- **Unit Tests:** Mandatory for API endpoints, introspection logic, and query generation.
- **Integration Tests:** Required for cross-module flows (e.g., NL → SQL → Result).

## 🚀 LLM-Specific Rules
- **Validation:** Always validate LLM outputs (SQL/Python) before execution via a "Verification Agent".
- **Fallbacks:** Implement fallback logic if query generation fails or returns invalid results.
- **Context:** Use **Weaviate** for RAG to provide relevant schema context to the LLM.

## ⚠️ What to Avoid
- Monolithic code or threading state across unrelated layers.
- Hardcoded values or "just-in-case" redundant logic.
- Silent changes without technical rationale.

