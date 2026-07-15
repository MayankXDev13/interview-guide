## Difference Between Monitoring and Observability

### Question

What is the difference between Monitoring and Observability?

### Short explanation of the question

Monitoring and observability are closely related but are **not the
same**. Monitoring tells you **when** something is wrong by collecting
predefined signals, while observability helps you understand **why** it
is wrong by analyzing telemetry such as logs, metrics, and traces.

### Answer

-   **Monitoring** is the process of collecting and tracking predefined
    metrics, logs, and alerts to determine whether a system is healthy.
-   **Observability** is the ability to understand the internal state of
    a system by analyzing telemetry data so that unknown problems can be
    investigated and resolved.

In simple terms:

-   **Monitoring answers:** *"Is something broken?"*
-   **Observability answers:** *"Why is it broken?"*

### Detailed explanation of the answer for readers' understanding

  ------------------------------------------------------------------------
  Aspect           Monitoring               Observability
  ---------------- ------------------------ ------------------------------
  **Goal**         Detect known issues      Investigate known and unknown
                                            issues

  **Focus**        Health checks and alerts Root cause analysis

  **Uses**         Dashboards, thresholds,  Logs, metrics, traces,
                   alerting                 correlations

  **Problem Type** Known failures           Unknown or complex failures

  **Output**       Alerts and notifications Deep insights into system
                                            behavior
  ------------------------------------------------------------------------

------------------------------------------------------------------------

### Monitoring Example

Suppose an application exposes these metrics:

-   CPU Usage
-   Memory Usage
-   Request Rate
-   HTTP Error Rate

Prometheus continuously scrapes these metrics.

If CPU usage exceeds 90%, Alertmanager sends an alert.

``` text
Application
      │
      ▼
Prometheus
      │
      ▼
Alertmanager
      │
      ▼
Slack / Email / PagerDuty
```

Monitoring successfully detects that a problem exists.

------------------------------------------------------------------------

### Observability Example

Users complain that API responses are taking 8 seconds.

Monitoring shows:

-   CPU usage is normal.
-   Memory usage is normal.
-   No error alerts.

Observability helps investigate further by correlating:

-   **Metrics** → Increased API latency.
-   **Logs** → Slow database queries.
-   **Traces** → Most request time spent in the payment service.

The root cause is identified as a slow database query rather than a CPU
issue.

------------------------------------------------------------------------

### The Three Pillars of Observability

1.  **Metrics**
    -   Numeric measurements over time.
    -   Example: CPU usage, memory, request latency.
2.  **Logs**
    -   Timestamped records of application events.
    -   Useful for debugging.
3.  **Traces**
    -   Follow a request across multiple services.
    -   Identify where latency is introduced.

------------------------------------------------------------------------

### Common Tools

  Monitoring           Observability
  -------------------- ---------------
  Prometheus           OpenTelemetry
  Alertmanager         Jaeger
  Grafana              Tempo
  Node Exporter        Loki
  kube-state-metrics   Elasticsearch

------------------------------------------------------------------------

### Typical interview answer

> Monitoring tells us whether a system is healthy by collecting
> predefined metrics and generating alerts. Observability goes further
> by using logs, metrics, and traces to determine why an issue occurred,
> including problems that were not anticipated when monitoring rules
> were created.

### Key takeaways

-   Monitoring detects problems.
-   Observability explains problems.
-   Monitoring is a subset of observability.
-   Logs, metrics, and traces together provide full visibility into
    distributed systems.