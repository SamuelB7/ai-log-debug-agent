# Observabilidade

Stack local:

| Componente | Uso |
| --- | --- |
| OpenTelemetry Collector | Recebe traces/metrics via OTLP |
| Jaeger | Visualizacao de traces |
| Prometheus | Coleta metricas expostas pelo collector |
| Grafana | Dashboards locais |

OTLP HTTP: `http://localhost:4318`

OTLP gRPC: `localhost:4317`

