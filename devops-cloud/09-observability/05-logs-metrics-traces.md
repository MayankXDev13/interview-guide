## Difference Between Logs, Metrics, and Traces

### Question

What is the difference between Logs, Metrics, and Traces?

### Short explanation of the question

This question tests your understanding of the **three pillars of
observability**. Logs, metrics, and traces provide different types of
telemetry data that work together to help monitor, troubleshoot, and
optimize applications, especially in distributed systems.

### Answer

-   **Logs** are detailed records of events that occur in an application
    or system.
-   **Metrics** are numerical measurements collected over time that help
    monitor the health and performance of a system.
-   **Traces** follow a single request as it travels through multiple
    services, showing the complete execution path and latency.

Together, they provide complete visibility into application behavior.

### Detailed explanation of the answer for readers' understanding

  --------------------------------------------------------------------------
  Aspect             Logs            Metrics              Traces
  ------------------ --------------- -------------------- ------------------
  **Data Type**      Event records   Numerical values     Request execution
                                                          path

  **Purpose**        Debugging and   Monitoring and       Root cause
                     auditing        alerting             analysis

  **Storage**        Loki,           Prometheus           Jaeger, Tempo,
                     Elasticsearch                        Zipkin

  **Example**        Login failed    CPU usage = 80%      API → Auth →
                                                          Payment → DB

  **Volume**         High            Low                  Medium
  --------------------------------------------------------------------------

------------------------------------------------------------------------

## 1. Logs

Logs capture events that occur in an application.

Example log:

``` text
2026-07-15 10:15:23 INFO Order created
Order ID: 1001
Customer: Alice
Status: Success
```

Logs typically contain:

-   Timestamp
-   Log level (INFO, WARN, ERROR)
-   Message
-   Request ID or Trace ID
-   Additional metadata

Logs are mainly used for:

-   Debugging
-   Error investigation
-   Security auditing
-   Application troubleshooting

------------------------------------------------------------------------

## 2. Metrics

Metrics are numeric values collected continuously over time.

Examples:

-   CPU usage
-   Memory usage
-   Request rate
-   API latency
-   HTTP 5xx errors
-   Pod restarts

Example Prometheus metrics:

``` text
http_requests_total
node_cpu_seconds_total
container_memory_usage_bytes
```

Metrics are mainly used for:

-   Dashboards
-   Alerting
-   Capacity planning
-   Performance monitoring

------------------------------------------------------------------------

## 3. Traces

Traces show how a single request moves through multiple services.

Example:

``` text
User Request
      │
      ▼
API Gateway
      │
      ▼
Authentication Service
      │
      ▼
Order Service
      │
      ▼
Payment Service
      │
      ▼
Database
```

Each step is called a **span**.

A complete collection of spans forms a **trace**.

Traces help answer:

-   Which service is slow?
-   Where did the request fail?
-   How long did each service take?

------------------------------------------------------------------------

## Real-world Example

A user reports that placing an order takes 8 seconds.

### Metrics show:

-   Request latency increased.
-   CPU and memory are normal.

### Logs show:

-   No application errors.
-   Slow SQL query messages.

### Traces show:

-   API Gateway: 20 ms
-   Authentication: 40 ms
-   Order Service: 120 ms
-   Payment Service: 5.8 s
-   Database: 5.5 s

The trace clearly identifies the database query in the payment service
as the bottleneck.

------------------------------------------------------------------------

## Common Tools

  Telemetry   Popular Tools
  ----------- -----------------------------------------------
  Logs        Loki, Elasticsearch, Fluent Bit
  Metrics     Prometheus, Node Exporter, kube-state-metrics
  Traces      Jaeger, Grafana Tempo, Zipkin, OpenTelemetry

------------------------------------------------------------------------

## Typical interview answer

> Logs record detailed events, metrics provide numerical measurements
> for monitoring, and traces follow a request across multiple services.
> Metrics help detect problems, logs provide detailed context, and
> traces identify where latency or failures occur in distributed
> systems. Together, they form the three pillars of observability.

### Best practices

-   Use structured logs with request or trace IDs.
-   Monitor infrastructure and application metrics.
-   Enable distributed tracing for microservices.
-   Correlate logs, metrics, and traces during incident investigation.

### Key takeaways

-   Logs answer **"What happened?"**
-   Metrics answer **"How is the system performing?"**
-   Traces answer **"Where did the request spend its time?"**
-   Combining all three provides complete observability for modern
    distributed applications.