# CRITICAL_CONSTRAINTS: BizCopilot

## 🛡️ Security & Safety
1. **SQL Injection:** Agents must use parameterized queries or strict validation layers. Never execute raw strings directly from LLM without a verification step.
2. **Sandbox Isolation:** Python execution must have NO network access and limited disk/CPU usage to prevent DoS or data exfiltration.
3. **Data Privacy:** One user MUST NOT be able to query another user's `user_data` tables. Enforcement at the API and Database levels.

## ⚖️ Performance
1. **Latency:** Total round-trip for a query should be < 5 seconds.
2. **File Size:** Initial MVP upload limit: 50MB per CSV.
3. **Concurrent Queries:** System must handle at least 10 concurrent AI sessions per standard node.

## 📉 Reliability
1. **Hallucination Mitigation:** Every SQL query must be "dry-run" or validated against the schema before execution.
2. **Fallback:** If the AI fails to generate a query, return a clear "I'm having trouble understanding that" with suggestions on how to rephrase.
