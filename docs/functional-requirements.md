# Requisitos Funcionais - DebugOps Agent

Documento derivado de `ai_log_debug_agent.md`.

Use os checkboxes para marcar requisitos conforme forem implementados. Cada item tem ID estável, nome e descrição.

## Admin Web Panel

- [ ] **ADM-001 - Login de usuário**  
  Descrição: permitir que usuários acessem o painel administrativo por fluxo de autenticação.

- [ ] **ADM-002 - Encerramento de sessão**  
  Descrição: permitir logout e invalidação visual da sessão ativa no painel.

- [ ] **ADM-003 - Rotas protegidas**  
  Descrição: bloquear telas administrativas para usuários não autenticados.

- [ ] **ADM-004 - Chat com agente de IA**  
  Descrição: permitir envio de perguntas em linguagem natural para investigar logs, erros, traces e incidentes.

- [ ] **ADM-005 - Exibição de respostas do agente**  
  Descrição: mostrar respostas técnicas do agente com texto estruturado, evidências, logs relacionados e próximos passos.

- [ ] **ADM-006 - Histórico de conversas**  
  Descrição: listar conversas anteriores e permitir retomada de uma investigação salva.

- [ ] **ADM-007 - Detalhes da conversa**  
  Descrição: exibir mensagens do usuário, respostas do agente, tools usadas e contexto retornado.

- [ ] **ADM-008 - Visualização de logs relacionados**  
  Descrição: mostrar logs retornados pelo agente ou pela busca direta, preservando campos importantes como serviço, ambiente, nível, timestamp, request ID e trace ID.

- [ ] **ADM-009 - Filtros de logs**  
  Descrição: permitir filtrar logs por serviço, ambiente, nível, período, mensagem, request ID e trace ID.

- [ ] **ADM-010 - Tela de incidentes**  
  Descrição: listar incidentes e relatórios gerados durante investigações.

- [ ] **ADM-011 - Detalhe de investigação**  
  Descrição: apresentar uma visão consolidada da investigação com pergunta inicial, evidências, logs, hipótese de causa raiz e relatório gerado.

- [ ] **ADM-012 - Geração de issue no GitHub**  
  Descrição: oferecer ação para solicitar criação de issue no GitHub a partir de um relatório de investigação.

- [ ] **ADM-013 - Estados de carregamento e erro**  
  Descrição: informar quando consultas, respostas do agente e buscas de logs estiverem carregando, vazias ou com erro.

- [ ] **ADM-014 - Navegação principal**  
  Descrição: disponibilizar navegação para chat, histórico, logs, incidentes e detalhes de investigação.

## Backend API / BFF

- [x] **BFF-001 - Autenticação de usuários**  
  Descrição: expor endpoints para autenticar usuários e emitir credenciais de acesso.

- [x] **BFF-002 - Autorização de requisições**  
  Descrição: validar credenciais em rotas protegidas e impedir acesso não autorizado.

- [x] **BFF-003 - Gerenciamento de usuários**  
  Descrição: manter dados básicos de usuários necessários para autenticação, autoria e auditoria.

- [x] **BFF-004 - Controle de permissões**  
  Descrição: permitir diferenciação de acessos para ações administrativas, consultas e integrações externas.

- [x] **BFF-005 - Persistência de conversas**  
  Descrição: salvar conversas iniciadas pelo usuário, incluindo mensagens enviadas e respostas recebidas do agente.

- [x] **BFF-006 - Persistência de mensagens**  
  Descrição: registrar cada mensagem com autoria, ordem, timestamp e vínculo com a conversa.

- [x] **BFF-007 - Proxy seguro para AI Agent Service**  
  Descrição: receber mensagens do painel, persistir o pedido e encaminhar a solicitação ao serviço de IA sem expor o serviço diretamente ao frontend.

- [x] **BFF-008 - Persistência de respostas do agente**  
  Descrição: salvar resposta final, evidências, logs relacionados, tools usadas e metadados da execução.

- [x] **BFF-009 - Consulta de logs salvos**  
  Descrição: expor API para consultar logs por filtros estruturados e retornar resultados para o painel.

- [x] **BFF-010 - Persistência de incidentes**  
  Descrição: salvar incidentes gerados a partir das investigações, incluindo título, descrição, severidade, evidências e status.

- [x] **BFF-011 - Persistência de relatórios técnicos**  
  Descrição: salvar relatórios de incidente produzidos pelo agente para consulta posterior.

- [x] **BFF-012 - Auditoria de ações do agente**  
  Descrição: registrar ações executadas pelo agente, incluindo tool chamada, parâmetros principais, usuário solicitante e resultado.

- [x] **BFF-013 - Integração com GitHub Issue Tool**  
  Descrição: receber solicitação do painel ou do agente e encaminhar criação de issue no GitHub quando configurado.

- [x] **BFF-014 - Cache e estado operacional com Redis**  
  Descrição: usar Redis para necessidades operacionais do backend, como cache, filas auxiliares ou controle de estado temporário.

- [x] **BFF-015 - Health check do backend**  
  Descrição: expor endpoint de saúde para validar que o serviço está disponível no ambiente local e em deploy futuro.

## Log Ingestor API

- [x] **ING-001 - Endpoint HTTP de ingestão**  
  Descrição: receber logs enviados por aplicações monitoradas via endpoint HTTP.

- [x] **ING-002 - Suporte a logs JSON**  
  Descrição: aceitar payloads de log em JSON como formato principal de ingestão.

- [x] **ING-003 - Validação de payload**  
  Descrição: validar campos obrigatórios, tipos de dados e formato antes de aceitar um log.

- [x] **ING-004 - Normalização inicial de logs**  
  Descrição: padronizar campos recebidos para um formato comum antes de publicar na fila.

- [x] **ING-005 - Autenticação por API key**  
  Descrição: exigir chave de API para impedir ingestão não autorizada.

- [x] **ING-006 - Rate limiting de ingestão**  
  Descrição: limitar volume de requisições por origem ou API key para proteger o serviço.

- [x] **ING-007 - Envio para fila Redis/BullMQ**  
  Descrição: publicar logs válidos em fila assíncrona para processamento pelo worker.

- [x] **ING-008 - Resposta de aceite de ingestão**  
  Descrição: retornar status claro indicando se o log foi aceito, rejeitado ou enfileirado.

- [x] **ING-009 - Tratamento de erros de ingestão**  
  Descrição: retornar mensagens de erro seguras e úteis para payload inválido, autenticação falha e indisponibilidade da fila.

- [x] **ING-010 - Health check do ingestor**  
  Descrição: expor endpoint de saúde para validar disponibilidade do serviço.

## Log Processor Worker

- [x] **WRK-001 - Consumo assíncrono da fila**  
  Descrição: consumir logs publicados pelo Log Ingestor na fila Redis/BullMQ.

- [x] **WRK-002 - Retry de processamento**  
  Descrição: permitir nova tentativa para logs que falharem por erro transitório.

- [x] **WRK-003 - Registro de falhas definitivas**  
  Descrição: registrar logs que não puderem ser processados após as tentativas configuradas.

- [x] **WRK-004 - Normalização completa de logs**  
  Descrição: consolidar campos do log em formato consistente para busca e persistência.

- [x] **WRK-005 - Extração de campos importantes**  
  Descrição: extrair serviço, ambiente, nível, mensagem, timestamp, request ID, trace ID e metadados relevantes.

- [x] **WRK-006 - Detecção de stack trace**  
  Descrição: identificar stack traces em logs e separar esse conteúdo para busca e análise.

- [x] **WRK-007 - Indexação no OpenSearch**  
  Descrição: gravar logs processados no OpenSearch para busca eficiente por filtros e texto.

- [x] **WRK-008 - Persistência de metadados no PostgreSQL**  
  Descrição: salvar metadados necessários para histórico, auditoria, agrupamentos e relacionamento com incidentes.

- [x] **WRK-009 - Agrupamento básico de erros semelhantes**  
  Descrição: identificar erros parecidos com base em mensagem, stack trace ou assinatura normalizada.

- [x] **WRK-010 - Idempotência de processamento**  
  Descrição: evitar duplicidade quando o mesmo log ou job for processado mais de uma vez.

- [x] **WRK-011 - Logs operacionais do worker**  
  Descrição: registrar início, sucesso, falha e tempo de processamento de cada job.

## AI Agent Service

- [ ] **AGT-001 - Endpoint de conversa**  
  Descrição: expor endpoint para receber perguntas do usuário e retornar respostas do agente.

- [ ] **AGT-002 - Gerenciamento de estado da conversa**  
  Descrição: manter contexto mínimo da conversa para interpretar perguntas de acompanhamento.

- [ ] **AGT-003 - Interpretação de intenção**  
  Descrição: transformar pergunta em linguagem natural em intenção de investigação.

- [ ] **AGT-004 - Seleção de tools**  
  Descrição: decidir quais ferramentas internas devem ser usadas para responder a pergunta.

- [ ] **AGT-005 - Tool `search_logs`**  
  Descrição: buscar logs por período, serviço, nível, mensagem, request ID ou trace ID.

- [ ] **AGT-006 - Tool `aggregate_errors`**  
  Descrição: agrupar erros semelhantes e contar frequência por assinatura, serviço e período.

- [ ] **AGT-007 - Tool `get_trace_timeline`**  
  Descrição: montar linha do tempo de eventos relacionados a um request ID ou trace ID.

- [ ] **AGT-008 - Tool `search_docs`**  
  Descrição: consultar documentação técnica indexada no serviço de RAG.

- [ ] **AGT-009 - Tool `generate_incident_report`**  
  Descrição: gerar relatório técnico com resumo, impacto, evidências, hipótese e próximos passos.

- [ ] **AGT-010 - Tool `create_github_issue`**  
  Descrição: criar issue no GitHub a partir da investigação e do relatório técnico.

- [ ] **AGT-011 - Geração de hipótese de causa raiz**  
  Descrição: propor causa mais provável para erro ou incidente com base em logs, traces e documentação.

- [ ] **AGT-012 - Resposta com evidências**  
  Descrição: retornar resposta explicável com referências aos logs, trechos de documentação e dados usados.

- [ ] **AGT-013 - Sugestão de próximos passos**  
  Descrição: sugerir ações técnicas para continuar investigação, mitigar incidente ou abrir correção.

- [ ] **AGT-014 - Integração com OpenSearch**  
  Descrição: consultar dados de logs por meio da tool de busca ou camada equivalente.

- [ ] **AGT-015 - Integração com banco relacional**  
  Descrição: acessar dados necessários de conversas, incidentes ou relatórios quando a investigação exigir.

- [ ] **AGT-016 - Integração com provedor de IA**  
  Descrição: usar OpenAI API ou provedor compatível para execução do raciocínio do agente.

- [ ] **AGT-017 - Tratamento de falhas de tools**  
  Descrição: responder de forma controlada quando uma tool falhar, sem ocultar que parte da investigação não foi concluída.

- [ ] **AGT-018 - Métricas de uso do agente**  
  Descrição: registrar métricas futuras de uso, custo de tokens e qualidade das respostas.

## Docs RAG Service

- [ ] **RAG-001 - Upload de documentos Markdown**  
  Descrição: permitir entrada de documentos Markdown para compor a base técnica consultável.

- [ ] **RAG-002 - Importação de documentação técnica**  
  Descrição: aceitar documentos do projeto para indexação, incluindo guias, contratos, arquitetura e runbooks.

- [ ] **RAG-003 - Processamento de documentos**  
  Descrição: quebrar documentos em trechos pesquisáveis com metadados de origem.

- [ ] **RAG-004 - Geração de embeddings**  
  Descrição: transformar trechos de documentação em vetores usando provedor configurado.

- [ ] **RAG-005 - Indexação vetorial no Qdrant**  
  Descrição: salvar embeddings e metadados no banco vetorial para busca semântica.

- [ ] **RAG-006 - Busca semântica de documentação**  
  Descrição: retornar trechos relevantes de documentação para uma pergunta ou contexto de investigação.

- [ ] **RAG-007 - Resposta com fontes**  
  Descrição: incluir referência do documento, título ou caminho de origem nos resultados retornados.

- [ ] **RAG-008 - Reindexação de documentos**  
  Descrição: permitir atualizar documentos já indexados quando o conteúdo mudar.

- [ ] **RAG-009 - API para tool `search_docs`**  
  Descrição: expor endpoint consumível pelo AI Agent Service para pesquisa de documentação.

- [ ] **RAG-010 - Health check do RAG**  
  Descrição: expor endpoint de saúde para validar disponibilidade do serviço.

## Repositório Agregador / Ambiente Local

- [ ] **INF-001 - Submodules dos serviços**  
  Descrição: manter cada serviço como submodule Git dentro de `services/`.

- [ ] **INF-002 - Docker Compose local**  
  Descrição: subir todos os serviços e dependências com um único `docker compose up`.

- [ ] **INF-003 - Variáveis de ambiente de exemplo**  
  Descrição: manter `.env.example` com variáveis necessárias para rodar o projeto localmente.

- [ ] **INF-004 - PostgreSQL local**  
  Descrição: disponibilizar banco relacional local para backend, histórico, incidentes e metadados.

- [ ] **INF-005 - Redis local**  
  Descrição: disponibilizar Redis para BullMQ, filas e necessidades operacionais.

- [ ] **INF-006 - OpenSearch local**  
  Descrição: disponibilizar OpenSearch para indexação e busca de logs.

- [ ] **INF-007 - Qdrant local**  
  Descrição: disponibilizar banco vetorial para RAG de documentação.

- [ ] **INF-008 - Observabilidade local**  
  Descrição: disponibilizar OpenTelemetry Collector, Jaeger, Prometheus e Grafana no ambiente local.

- [ ] **INF-009 - Documentação de desenvolvimento local**  
  Descrição: documentar portas, comandos, dependências e fluxo para subir o ambiente.

- [ ] **INF-010 - Documentação de arquitetura**  
  Descrição: manter documentação de arquitetura, contratos, modelo de dados, tools do agente e observabilidade.

- [ ] **INF-011 - Persistência local por volumes**  
  Descrição: configurar volumes Docker para preservar dados de PostgreSQL, Redis, OpenSearch, Qdrant, Prometheus e Grafana.

- [ ] **INF-012 - Comandos de validação local**  
  Descrição: documentar comandos para validar submodules, compose e health checks dos serviços.
