# Node RAG Anime Recommendation Web App

A basic Node.js application implementing a RAG chatbot for anime recommendations.

Data is sourced from the AniList GraphQL API and stored in Qdrant as a vector database. Uses LangChain and HuggingFace JS libraries for orchestration and retrieval.

## Models Used

- **Embeddings**
  - `nomic-embed-text`
  - Hosted locally via Ollama

- **Chat LLM**
  - `openai/gpt-oss-120b`
  - Served via Groq API

- **Reranker**
  - `BAAI/bge-reranker-v2-m3`
  - Provided via HuggingFace Inference API

---

## Installation

### 1. Clone repository
```bash
git clone https://github.com/Alcimidius/node_rag.git
```

### 2. Install dependencies
```bash
npm install
```

### 3. Start frontend
```bash
npm run client
```

### 4. Start backend, database, and Ollama services
```bash
docker compose up
```

### 5. Pull embedding model (Ollama)
```bash
docker exec ollama ollama pull nomic-embed-text
```

### 6. Seed database
```bash
docker exec backend_server node apps/backend/util/databaseSetup.js <n>
```
- `<n>` = number of entries pulled from AniList

---

## Environment Variables

### Backend `.env` (apps/backend/.env)
```env
SERVER_PORT=9000
GROQ_API_KEY=key
HF_API_KEY=key
OLLAMA_URL=http://127.0.0.1:12434
QDRANT_DATABASE_URL=http://127.0.0.1:6333
```

### Docker `.env.docker` (apps/backend/.env.docker)
```env
SERVER_PORT=9000
GROQ_API_KEY=key
HF_API_KEY=key
OLLAMA_URL=http://ollama:11434
QDRANT_DATABASE_URL=http://database:6333
```

---

## License

MIT — https://choosealicense.com/licenses/mit/
