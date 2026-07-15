## Tools Used to Build an Observability Stack

### Question

Which tools have you used to build an observability stack?

### Short explanation of the question

This question evaluates your practical knowledge of observability tools.
Interviewers want to understand which tools you have used for collecting
logs, metrics, traces, visualization, and alerting in production
environments.

### Answer

In a Kubernetes-based environment, I have used the following tools:

-   **Prometheus** -- Metrics collection
-   **Grafana** -- Dashboards and visualization
-   **Alertmanager** -- Alert routing and notifications
-   **Node Exporter** -- Node-level metrics
-   **kube-state-metrics** -- Kubernetes object metrics
-   **cAdvisor** -- Container metrics
-   **Fluent Bit** -- Log collection
-   **Loki** -- Log storage
-   **OpenTelemetry** -- Instrumentation
-   **Jaeger / Grafana Tempo** -- Distributed tracing

Together, these tools provide complete observability across
infrastructure and applications.

### Detailed explanation of the answer for readers' understanding

A typical observability architecture:

``` text
Applications
      │
      ├── Metrics (/metrics)
      ├── Logs
      └── Traces
             │
             ▼
   OpenTelemetry SDK
      │
      ├──────────────┐
      ▼              ▼
 Prometheus      Fluent Bit
      │              │
      ▼              ▼
 Alertmanager      Loki
      │              │
      └──────┬───────┘
             ▼
          Grafana
             │
             ▼
      Jaeger / Tempo
```

------------------------------------------------------------------------

## 1. Prometheus

Purpose:

-   Collects time-series metrics
-   Scrapes `/metrics` endpoints
-   Stores infrastructure and application metrics

Example metrics:

-   CPU usage
-   Memory usage
-   Request latency
-   HTTP request rate

------------------------------------------------------------------------

## 2. Grafana

Purpose:

-   Creates dashboards
-   Visualizes metrics and logs
-   Correlates telemetry
-   Supports alerting

Common dashboards:

-   Kubernetes Cluster
-   Node Health
-   API Performance
-   Database Performance

------------------------------------------------------------------------

## 3. Alertmanager

Purpose:

-   Receives alerts from Prometheus
-   Deduplicates alerts
-   Groups related alerts
-   Sends notifications

Notification channels:

-   Slack
-   Email
-   PagerDuty
-   Microsoft Teams

------------------------------------------------------------------------

## 4. Node Exporter

Collects Linux host metrics:

-   CPU
-   Memory
-   Disk
-   Filesystem
-   Network

------------------------------------------------------------------------

## 5. kube-state-metrics

Provides Kubernetes resource metrics such as:

-   Pod status
-   Deployment replicas
-   Node conditions
-   StatefulSets
-   DaemonSets

------------------------------------------------------------------------

## 6. cAdvisor

Collects container metrics:

-   CPU usage
-   Memory usage
-   Network traffic
-   Restart count

------------------------------------------------------------------------

## 7. Fluent Bit

Collects application and container logs from Kubernetes and forwards
them to logging backends such as Loki or Elasticsearch.

------------------------------------------------------------------------

## 8. Loki

Stores logs efficiently and integrates directly with Grafana for
searching and correlation.

------------------------------------------------------------------------

## 9. OpenTelemetry

Provides standard instrumentation for applications.

It collects:

-   Metrics
-   Logs
-   Traces

without locking applications to a specific vendor.

------------------------------------------------------------------------

## 10. Jaeger / Grafana Tempo

Used for distributed tracing.

They help identify:

-   Slow microservices
-   Request flow
-   Latency bottlenecks
-   Failed service calls

------------------------------------------------------------------------

## Typical interview answer

> I have worked with Prometheus, Grafana, Alertmanager, Node Exporter,
> kube-state-metrics, cAdvisor, Fluent Bit, and Loki to build an
> observability stack. For distributed tracing, I have used
> OpenTelemetry with Jaeger or Grafana Tempo. This stack provides
> monitoring, centralized logging, tracing, dashboards, and alerting for
> Kubernetes-based applications.

### Best practices

-   Use Prometheus for metrics.
-   Use Grafana for dashboards.
-   Collect structured logs with Fluent Bit.
-   Centralize logs in Loki.
-   Instrument applications with OpenTelemetry.
-   Use distributed tracing for microservices.

### Key takeaways

-   Observability requires logs, metrics, and traces.
-   No single tool provides complete observability.
-   A modern Kubernetes stack commonly uses Prometheus, Grafana,
    Alertmanager, Fluent Bit, Loki, OpenTelemetry, and Jaeger or Tempo
    together.