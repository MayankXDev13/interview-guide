## Users Report Slowness in the Application. Logs Don't Show Errors and CPU is Good. How Would You Fix It?

### Question

Users report slowness in the application. Logs don't show errors, and
CPU usage is normal. How would you identify and fix the issue?

### Short explanation of the question

This is a real-world troubleshooting scenario. The interviewer wants to
evaluate your debugging methodology rather than a single solution. Since
logs and CPU usage do not indicate a problem, you should use
observability tools to investigate latency across the entire request
path.

### Answer

I would troubleshoot the issue systematically by analyzing **metrics,
logs, traces, infrastructure, and dependencies**.

Since CPU usage is healthy and logs do not show errors, I would suspect:

-   Slow database queries
-   Network latency
-   External API delays
-   Lock contention
-   High request latency in downstream services
-   Disk or storage bottlenecks

Distributed tracing is usually the fastest way to identify where the
request is spending time.

### Detailed explanation of the answer for readers' understanding

A typical troubleshooting workflow:

``` text
User Reports Slow API
         │
         ▼
Check Grafana Dashboards
         │
         ▼
Review Prometheus Metrics
         │
         ▼
Analyze Distributed Traces
         │
         ▼
Inspect Logs
         │
         ▼
Identify Root Cause
         │
         ▼
Apply Fix
```

------------------------------------------------------------------------

## Step 1 --- Verify Application Metrics

Start with Grafana dashboards.

Check:

-   Request latency
-   Request rate
-   Error rate
-   Active requests

Useful Prometheus metrics:

``` text
http_request_duration_seconds
http_requests_total
http_requests_in_progress
```

If latency has increased while errors remain low, the application is
slow rather than failing.

------------------------------------------------------------------------

## Step 2 --- Check Infrastructure Metrics

Even if CPU usage is normal, investigate:

-   Memory usage
-   Disk I/O
-   Network throughput
-   Network latency
-   File system utilization

Example metrics:

``` text
node_memory_MemAvailable_bytes
node_disk_io_time_seconds_total
node_network_receive_bytes_total
```

------------------------------------------------------------------------

## Step 3 --- Analyze Distributed Traces

Open Jaeger or Grafana Tempo.

Follow a slow request across services.

Example:

``` text
API Gateway
      │ 20 ms
      ▼
Authentication
      │ 35 ms
      ▼
Order Service
      │ 120 ms
      ▼
Payment Service
      │ 5.7 s
      ▼
Database
```

The trace immediately identifies the slow component.

------------------------------------------------------------------------

## Step 4 --- Review Logs

Search logs in Loki or Elasticsearch.

Look for:

-   Slow SQL queries
-   Connection pool exhaustion
-   Timeout messages
-   Retry loops
-   External API latency

Logs may not contain errors but often reveal performance warnings.

------------------------------------------------------------------------

## Step 5 --- Check Database Performance

Verify:

-   Slow queries
-   Missing indexes
-   Lock contention
-   High connection count
-   Long-running transactions

Database latency is a common cause of application slowness.

------------------------------------------------------------------------

## Step 6 --- Check External Dependencies

If the application calls:

-   Payment gateways
-   Authentication providers
-   Third-party APIs

Measure their response times.

Distributed traces usually expose slow external calls.

------------------------------------------------------------------------

## Possible Root Causes

  Symptom                         Possible Cause
  ------------------------------- -------------------------------------
  High latency, normal CPU        Slow database query
  High latency after deployment   Inefficient application code
  Slow only for some requests     Missing database index
  High network latency            Service-to-service networking issue
  Slow external API               Third-party dependency

------------------------------------------------------------------------

## Example Investigation

Observations:

-   CPU: 30%
-   Memory: 45%
-   Error rate: 0%
-   API latency: 7 seconds

Trace:

``` text
Gateway        20 ms
Auth           30 ms
Order Service  80 ms
Database     6.8 seconds
```

Root cause:

A missing database index caused full table scans.

Fix:

-   Add the required index.
-   Optimize the SQL query.
-   Monitor latency after deployment.

------------------------------------------------------------------------

## Typical interview answer

> I would begin with Grafana dashboards to verify latency and traffic
> metrics, then review Prometheus metrics for infrastructure health.
> Since CPU and logs appear normal, I would analyze distributed traces
> using Jaeger or Tempo to identify the slow service. Next, I would
> inspect logs for warnings, investigate database performance, and check
> external dependencies. After identifying the bottleneck, I would
> implement the fix and verify that latency returned to normal.

### Best practices

-   Follow a structured troubleshooting process.
-   Correlate metrics, logs, and traces.
-   Investigate dependencies, not just the application.
-   Validate the fix using dashboards and traces after deployment.

### Key takeaways

-   Normal CPU usage does not rule out performance problems.
-   Distributed tracing is one of the most effective ways to locate
    latency in microservices.
-   Database queries and external APIs are common bottlenecks.
-   Always confirm that the issue is resolved by monitoring
    post-deployment metrics.