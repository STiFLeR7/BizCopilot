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
- **Alembic:** Used for all `public` schema migrations.
- **Dynamic Migration:** Custom logic for `user_data` table creation (not managed by Alembic).
