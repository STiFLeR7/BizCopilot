# INTEGRATION_SPECS: BizCopilot

## 📡 Backend <=> Frontend Contract

### 1. Unified Response Format
```json
{
  "success": true,
  "session_id": "uuid",
  "data": {
    "text_content": "Your sales grew by 15% last month.",
    "raw_data": [ ... ],
    "visualization": {
      "type": "bar",
      "x_axis": "month",
      "y_axis": "revenue",
      "series": "sales_2023"
    }
  },
  "error": null
}
```

### 2. Streaming (Optional for V2)
Websockets or Server-Sent Events (SSE) for real-time agent "thinking" updates.

## 📱 Mobile Specifics
- **Auth:** OAuth2 with Bearer Tokens.
- **Notifications:** Firebase Cloud Messaging (FCM) for insight alerts.

## 🗄️ Database Integration
- **Alembic:** Used for all application-level schema migrations (e.g., users, logs).
- **Introspection:** Automated metadata extraction from existing PostgreSQL databases (READ-ONLY).
- **Weaviate Indexing:** Sync protocol to refresh schema embeddings when connections are added/updated.

## 🚀 Deployment Contract
- **Architecture:** Cloud-Native Mirror using Docker Compose.
- **Environment Parity:** Local development containers match **GCP (Google Cloud Platform)** production environment.
- **Secrets:** Managed via `.env` locally and Secret Manager on GCP.
