# Desenvolvimento local

## Subir ambiente

```bash
cp .env.example .env
docker compose up --build
```

## Servicos

| Servico | Porta |
| --- | --- |
| Admin Web | 5173 |
| Backend API | 3000 |
| Log Ingestor | 3002 |
| AI Agent Service | 8000 |
| Docs RAG Service | 8001 |
| PostgreSQL | 5432 |
| Redis | 6379 |
| OpenSearch | 9200 |
| Qdrant | 6333 |
| Jaeger | 16686 |
| Prometheus | 9090 |
| Grafana | 3001 |

## Observacao

Este bootstrap nao contem regra de negocio. Endpoints e workers existem apenas para validar estrutura, runtime e conectividade basica.

