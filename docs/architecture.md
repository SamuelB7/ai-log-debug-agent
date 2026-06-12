# Arquitetura

O projeto usa um repositorio agregador com servicos separados em `services/`.

Fluxo previsto:

1. Aplicacoes monitoradas enviam logs para `log-ingestor`.
2. `log-ingestor` publica mensagens no Redis/BullMQ.
3. `log-worker` consome a fila e prepara persistencia em PostgreSQL/OpenSearch.
4. `admin-web` conversa com `backend-api`.
5. `backend-api` centraliza autenticacao futura, historico e chamadas para servicos de IA.
6. `ai-agent-service` orquestra ferramentas de investigacao.
7. `docs-rag-service` concentra busca vetorial em documentacao usando Qdrant.

