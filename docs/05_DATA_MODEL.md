# DATA_MODEL: BizCopilot

## 🗄️ PostgreSQL Schema Strategy

### 1. System Schema (`public`)
Stores application-level metadata.
- `users`: Auth credentials, roles, settings.
- `datasets`: Metadata about uploaded files (name, owner, original filename, table name mapping).
- `chat_sessions`: History of conversations for context retrieval.
- `queries`: Log of NL queries and their generated SQL/Python counterparts (for debugging/fine-tuning).

### 2. User Data Schema (`user_data`)
Stores the actual business data.
- **Dynamic Tables:** Every CSV upload is converted into a structured PostgreSQL table within this schema (e.g., `user_data.sales_2023_hill`).
- **Isolation:** Tables are prefixed or separated to prevent cross-user data leakage.

## 🧠 Vector Metadata (FAISS/Weaviate)
Stores semantic representations of the database schema:
- **Table Names & Descriptions:** "What does this table represent?"
- **Column Names & Samples:** "What kind of data is in 'order_status'?"
- **KPI Definitions:** Standard business definitions (e.g., "Churn Rate = Customers lost / Total customers").

## 🔄 Ingestion Pipeline
1. **Upload:** User sends CSV.
2. **Inference:** System infers types (Integer, Date, Text) using Pandas/Pydantic.
3. **Create:** `CREATE TABLE user_data.table_name (...)`
4. **Load:** `COPY` command to bulk load data into Postgres.
5. **Index:** Auto-generate indices on likely join/filter keys (ID, Date).
