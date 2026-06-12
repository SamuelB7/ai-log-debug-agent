# DebugOps Agent

Repositorio agregador do AI Log Debug Agent.

Este repo centraliza documentacao, infraestrutura local e os servicos que depois podem virar `git submodules`.

## Estrutura

```txt
services/
  admin-web/
  backend-api/
  log-ingestor/
  log-worker/
  ai-agent-service/
  docs-rag-service/
docs/
infra/
docker-compose.yml
```

## Rodar localmente

```bash
cp .env.example .env
docker compose up --build
```

Portas principais:

| Servico | URL |
| --- | --- |
| Admin Web | http://localhost:5173 |
| Backend API | http://localhost:3000/health |
| Log Ingestor | http://localhost:3002/health |
| AI Agent Service | http://localhost:8000/health |
| Docs RAG Service | http://localhost:8001/health |
| OpenSearch | http://localhost:9200 |
| Qdrant | http://localhost:6333 |
| Jaeger | http://localhost:16686 |
| Prometheus | http://localhost:9090 |
| Grafana | http://localhost:3001 |

## Submodules

Os servicos foram criados como pastas locais para bootstrap inicial. Quando os repos remotos existirem, use `.gitmodules.example` como base e converta `services/*` para submodules reais.

