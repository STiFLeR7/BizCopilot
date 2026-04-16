# 🤖 BizCopilot: Autonomous Business Analytics Engine

[![Architecture: Modular Monolith](https://img.shields.io/badge/Architecture-Modular_Monolith-blue.svg)](#-system-architecture)
[![Engine: LangGraph](https://img.shields.io/badge/Engine-LangGraph-orange.svg)](https://langchain-ai.github.io/langgraph/)
[![Database: PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-336791.svg)](https://www.postgresql.org/)

BizCopilot is a production-grade **Agentic Process Automation (APA)** platform designed to bridge the gap between raw unstructured business data and executive-level decision-making. Unlike static BI tools, BizCopilot employs a multi-agent orchestrator to dynamically generate SQL, execute sandboxed code, and synthesize narrative insights.

---

## 🏗️ System Architecture

The system is architected as a **Context-Aware Agentic Loop**, ensuring that every query is grounded in the specific schema and business logic of the user.

### 🧩 Core Component Layers

1.  **Orchestration Layer (LangGraph):** A stateful, directed acyclic graph (DAG) that manages the "Chain of Thought." It handles intent routing, self-correction logic, and multi-turn memory.
2.  **Intelligence Layer (Hybrid Specialist Agents):**
    *   **SQL Architect:** RAG-enhanced agent that transforms NL into optimized PostgreSQL.
    *   **Python Analyst:** Executes in a **gVisor-style sandbox** for statistical modeling and predictive analysis.
    *   **Narrative Synthesizer:** Deterministic post-processing of data into human-centric business value.
3.  **Data Persistence Layer:**
    *   **Metadata DB (Postgres):** Manages sessions, users, and audit logs.
    *   **Dynamic Lakehouse (Postgres + user_data schema):** Decoupled storage where user-uploaded CSVs are transformed into queryable relational tables.
    *   **Vector Index (FAISS):** Stores semantic embeddings of the database schema for sub-second context retrieval.

---

## 🤖 Agentic Design Patterns

BizCopilot implements several advanced APA patterns to ensure reliability in production:

*   **Self-Healing SQL:** If an LLM-generated query fails, the error trace is fed back into the `SQL Architect` for a deterministic retry.
*   **Verification Gatekeeper:** A non-generative validation layer that audits SQL for forbidden operations (e.g., `DROP`, `DELETE`) and ensures Python imports are restricted to safe libraries (`pandas`, `numpy`, `scipy`).
*   **Dynamic Schema Injection (RAG):** Instead of dumping the whole schema into a prompt, we use semantic search to inject only the relevant tables, minimizing token noise and hallucination.

---

## 🛠️ Tech Stack & Engineering Standards

| Category | Technology | Rationale |
| :--- | :--- | :--- |
| **Backend** | FastAPI | High-performance async execution for I/O bound LLM calls. |
| **LLM Engine** | GPT-4o / Claude 3.5 | SOTA reasoning for code generation and synthesis. |
| **State Mgmt** | LangGraph | Explicit control over agent transitions vs. "Black Box" agents. |
| **Sandbox** | Restricted Subprocess | Prevents data exfiltration and resource exhaustion. |
| **Mobile** | Kotlin / Compose | Native performance for real-time conversational UI. |

---

## 🚀 Execution Roadmap (The 8-Week Sprint)

*   **Phase 1: Foundation** - Dynamic Ingestion Engine & Schema Mapping.
*   **Phase 2: Intelligence** - SQL-Retriever & RAG implementation.
*   **Phase 3: Analysis** - Python Sandbox & Visualization specs.
*   **Phase 4: Integration** - Mobile E2E flow & Production hardening.

---

## 🔐 Security & Governance

As a **Forward Deployed Engineer** (FDE) focused project, security is a first-class citizen:
*   **Logical Isolation:** Each user's data exists in a distinct schema namespace.
*   **Ephemeral Environments:** Analytical code is executed in isolated processes with zero network egress.
*   **Auditability:** Every generated query and LLM "thought" is logged for compliance and fine-tuning.

---

## 👨‍💻 Contributing

This repository follows a **Single-Owner Module** pattern. 
- `/backend`: @Hill (AI/ML Lead)
- `/android`: @Yash (Mobile Lead)
- `/data`: @Krish (Data Lead)
- `/analytics`: @Kushank (Analysis Lead)

---

> *"BizCopilot is not a chatbot; it is a digital workforce for your data."*
