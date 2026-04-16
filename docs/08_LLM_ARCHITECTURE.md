# LLM_ARCHITECTURE: BizCopilot

## 🏗️ The Multi-Stage Pipeline

### Stage 1: Context Enrichment (RAG)
- **Task:** Retrieve relevant schema snippets.
- **Prompt:** "Given the user's question about 'monthly revenue', which tables from the list [sales, customers, products] are relevant?"
- **Output:** List of table/column metadata.

### Stage 2: Code/Query Generation
- **Task:** Write the technical instruction.
- **System Prompt:** Contains "You are a Senior PostgreSQL expert. Use CTEs for readability. Only use the provided schema."

### Stage 3: Verification Layer (The Critic)
- **Task:** Audit the generated code.
- **Checklist:**
    - Does the SQL join on correct keys?
    - Does the Python code use any forbidden libraries?
    - Is the visualization logic compatible with the result set?

### Stage 4: Synthesis
- **Task:** Human-centric delivery.
- **Tone:** Professional, concise, data-driven.

## 🔄 State Management (LangGraph)
- The graph maintains the "Conversation State."
- If a user says "And what about the month before?", the graph injects the previous SQL result as context.
