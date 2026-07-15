## How to Emit Custom Logs and Metrics in Your Application

### Question

How do you emit custom logs and metrics in your application?

### Short explanation of the question

This question tests whether you know how applications expose
**observability data**. Modern applications should generate meaningful
logs and custom metrics so operators can monitor health, troubleshoot
issues, and measure business events.

### Answer

Applications emit:

-   **Logs** by writing structured log messages using a logging library.
-   **Metrics** by exposing counters, gauges, histograms, or summaries
    through a metrics library such as Prometheus client libraries.

The observability stack then collects this telemetry for visualization
and alerting.

### Detailed explanation of the answer for readers' understanding

A typical observability flow is:

``` text
Application
   │
   ├── Structured Logs
   ├── Custom Metrics
   │
   ▼
Collector / Exporter
   │
   ├── Loki / Elasticsearch (Logs)
   └── Prometheus (Metrics)
           │
           ▼
        Grafana
```

------------------------------------------------------------------------

### Emitting Custom Logs

Applications should generate structured logs instead of plain text.

Example (Python):

``` python
import logging

logging.basicConfig(level=logging.INFO)

logging.info(
    "Order created",
    extra={
        "order_id": 101,
        "customer": "alice",
        "amount": 250
    }
)
```

Good logging practices:

-   Use structured (JSON) logs.
-   Include timestamps.
-   Include request IDs or trace IDs.
-   Log meaningful events.
-   Avoid logging secrets or passwords.

------------------------------------------------------------------------

### Emitting Custom Metrics

Prometheus client libraries allow applications to expose metrics.

Example (Python):

``` python
from prometheus_client import Counter, start_http_server

orders_created = Counter(
    "orders_created_total",
    "Total number of orders created"
)

start_http_server(8000)

orders_created.inc()
```

Prometheus scrapes:

``` text
http://application:8000/metrics
```

------------------------------------------------------------------------

### Types of Prometheus Metrics

  Metric Type   Purpose                  Example
  ------------- ------------------------ --------------------
  Counter       Only increases           Total API requests
  Gauge         Increases or decreases   Active users
  Histogram     Measures distribution    Request latency
  Summary       Calculates quantiles     Response time

------------------------------------------------------------------------

### Example Business Metrics

You can expose custom metrics such as:

-   Orders created
-   Payments completed
-   Failed logins
-   Cart checkouts
-   Messages processed
-   Queue length

These metrics help monitor both system health and business performance.

------------------------------------------------------------------------

### Kubernetes Example

``` text
Application
      │
      ▼
/metrics endpoint
      │
      ▼
Prometheus Scrapes
      │
      ▼
Grafana Dashboard
      │
      ▼
Alertmanager
```

------------------------------------------------------------------------

### Typical interview answer

> I use structured logging libraries to emit application logs and
> Prometheus client libraries to expose custom metrics through a
> `/metrics` endpoint. Prometheus scrapes these metrics, while logs are
> collected using tools such as Fluent Bit into Loki or Elasticsearch.
> Grafana is then used for dashboards and alerting.

### Key takeaways

-   Use structured logs for debugging.
-   Expose custom metrics using Prometheus client libraries.
-   Track both technical and business metrics.
-   Visualize metrics in Grafana and configure alerts for important
    thresholds.