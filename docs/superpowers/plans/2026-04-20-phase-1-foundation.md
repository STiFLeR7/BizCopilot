# BizCopilot Phase 1: Foundation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Initialize the BizCopilot project structure, setup a Docker-based environment with Weaviate, and implement the core logic for introspecting an existing PostgreSQL database and indexing its schema.

**Architecture:** A modular monolith structure with a FastAPI backend. Docker Compose manages the backend and Weaviate. The backend uses Google ADK for orchestration and connects to an external PostgreSQL instance (managed via PGAdmin4).

**Tech Stack:** Python 3.10+, FastAPI, Weaviate, Docker, Docker Compose, SQLAlchemy (for introspection).

---

### Task 1: Initialize Project Structure

**Files:**
- Create: `backend/main.py`
- Create: `backend/requirements.txt`
- Create: `.env`
- Create: `.gitignore`

- [ ] **Step 1: Create backend directory and basic FastAPI app**

```python
# backend/main.py
from fastapi import FastAPI

app = FastAPI(title="BizCopilot API")

@app.get("/health")
def health_check():
    return {"status": "healthy"}
```

- [ ] **Step 2: Create requirements.txt**

```text
fastapi
uvicorn
python-dotenv
weaviate-client
sqlalchemy
psycopg2-binary
pydantic-settings
```

- [ ] **Step 3: Create .env template**

```text
# .env
POSTGRES_HOST=host.docker.internal
POSTGRES_PORT=5432
POSTGRES_USER=postgres
POSTGRES_PASSWORD=@HillPatel07
POSTGRES_DB=postgres

WEAVIATE_URL=http://weaviate:8080
GEMINI_API_KEY=your_api_key_here
```

- [ ] **Step 4: Create .gitignore**

```text
__pycache__/
.env
.venv
.superpowers/
*.pyc
```

- [ ] **Step 5: Verify setup and commit**

Run: `ls -R`
Run: `git add . && git commit -m "chore: initial project structure and dependencies"`

---

### Task 2: Docker Compose Foundation

**Files:**
- Create: `docker-compose.yml`
- Create: `backend/Dockerfile`

- [ ] **Step 1: Create Dockerfile for backend**

```dockerfile
# backend/Dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

- [ ] **Step 2: Create docker-compose.yml**

```yaml
version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "8000:8000"
    env_file: .env
    extra_hosts:
      - "host.docker.internal:host-gateway"
    depends_on:
      - weaviate

  weaviate:
    image: semitechnologies/weaviate:1.24.1
    ports:
      - "8080:8080"
      - "50051:50051"
    environment:
      QUERY_DEFAULTS_LIMIT: 25
      AUTHENTICATION_ANONYMOUS_ACCESS_ENABLED: 'true'
      PERSISTENCE_DATA_PATH: '/var/lib/weaviate'
      DEFAULT_VECTORIZER_MODULE: 'none'
      ENABLE_MODULES: ''
      CLUSTER_HOSTNAME: 'node1'
```

- [ ] **Step 3: Verify Docker Compose can start (dry-run or build)**

Run: `docker compose build`
Expected: Successful build of backend image.

- [ ] **Step 4: Commit**

```bash
git add docker-compose.yml backend/Dockerfile
git commit -m "infra: add docker compose for backend and weaviate"
```

---

### Task 3: Configuration & Database Connection

**Files:**
- Create: `backend/config.py`
- Create: `backend/database.py`

- [ ] **Step 1: Implement configuration management**

```python
# backend/config.py
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    postgres_host: str
    postgres_port: int
    postgres_user: str
    postgres_password: str
    postgres_db: str
    weaviate_url: str
    gemini_api_key: str

    class Config:
        env_file = ".env"

settings = Settings()
```

- [ ] **Step 2: Implement database engine and session**

```python
# backend/database.py
from sqlalchemy import create_all, create_engine, inspect
from config import settings

DATABASE_URL = f"postgresql://{settings.postgres_user}:{settings.postgres_password}@{settings.postgres_host}:{settings.postgres_port}/{settings.postgres_db}"

engine = create_engine(DATABASE_URL)

def get_db_inspector():
    return inspect(engine)
```

- [ ] **Step 3: Test connection logic**

```python
# backend/test_db.py
from database import get_db_inspector

def test_connection():
    inspector = get_db_inspector()
    schemas = inspector.get_schema_names()
    print(f"Schemas found: {schemas}")
    assert len(schemas) > 0

if __name__ == "__main__":
    test_connection()
```

- [ ] **Step 4: Run test and commit**

Run: `python backend/test_db.py` (ensure local PG is running or env points correctly)
Run: `git add backend/config.py backend/database.py && git commit -m "feat: database connection and config management"`

---

### Task 4: Schema Introspection Service

**Files:**
- Create: `backend/services/introspection.py`

- [ ] **Step 1: Implement introspection logic**

```python
# backend/services/introspection.py
from database import get_db_inspector

def get_database_metadata():
    inspector = get_db_inspector()
    metadata = []
    
    for schema in inspector.get_schema_names():
        if schema in ['information_schema', 'pg_catalog']:
            continue
            
        for table_name in inspector.get_table_names(schema=schema):
            columns = []
            for column in inspector.get_columns(table_name, schema=schema):
                columns.append({
                    "name": column['name'],
                    "type": str(column['type']),
                    "nullable": column['nullable']
                })
            
            metadata.append({
                "schema": schema,
                "table": table_name,
                "columns": columns
            })
    return metadata
```

- [ ] **Step 2: Add test for introspection**

```python
# backend/test_introspection.py
from services.introspection import get_database_metadata

def test_introspection():
    metadata = get_database_metadata()
    assert isinstance(metadata, list)
    if metadata:
        print(f"Introspected {len(metadata)} tables.")
        print(f"Sample table: {metadata[0]['table']}")

if __name__ == "__main__":
    test_introspection()
```

- [ ] **Step 3: Run test and commit**

Run: `python backend/test_introspection.py`
Run: `git add backend/services/introspection.py && git commit -m "feat: database schema introspection service"`

---

### Task 5: Weaviate Indexing Service

**Files:**
- Create: `backend/services/vector_store.py`

- [ ] **Step 1: Implement Weaviate client and schema creation**

```python
# backend/services/vector_store.py
import weaviate
from config import settings

client = weaviate.Client(url=settings.weaviate_url)

def initialize_weaviate_schema():
    class_obj = {
        "class": "SchemaElement",
        "description": "Metadata about database tables and columns",
        "vectorizer": "none",
        "properties": [
            {"name": "schemaName", "dataType": ["text"]},
            {"name": "tableName", "dataType": ["text"]},
            {"name": "columnName", "dataType": ["text"]},
            {"name": "columnType", "dataType": ["text"]},
            {"name": "description", "dataType": ["text"]}
        ]
    }
    if not client.schema.contains(class_obj):
        client.schema.create_class(class_obj)

def index_metadata(metadata):
    with client.batch as batch:
        for table in metadata:
            for col in table['columns']:
                properties = {
                    "schemaName": table['schema'],
                    "tableName": table['table'],
                    "columnName": col['name'],
                    "columnType": col['type'],
                    "description": f"Table: {table['table']}, Column: {col['name']} ({col['type']})"
                }
                batch.add_data_object(properties, "SchemaElement")
```

- [ ] **Step 2: Create setup script to run everything**

```python
# backend/setup_foundation.py
from services.introspection import get_database_metadata
from services.vector_store import initialize_weaviate_schema, index_metadata

def main():
    print("Starting Foundation Setup...")
    metadata = get_database_metadata()
    print(f"Extracted metadata for {len(metadata)} tables.")
    
    initialize_weaviate_schema()
    print("Weaviate schema initialized.")
    
    index_metadata(metadata)
    print("Metadata indexed in Weaviate.")

if __name__ == "__main__":
    main()
```

- [ ] **Step 3: Run setup and verify**

Run: `docker compose up -d weaviate`
Run: `python backend/setup_foundation.py`
Run: `git add backend/services/vector_store.py backend/setup_foundation.py && git commit -m "feat: weaviate indexing for database schema"`
