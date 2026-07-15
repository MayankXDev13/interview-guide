## Have You Worked on Observability? Explain What You Did.

### Question

Have you worked on Observability? If yes, explain what you did.

### Short explanation of the question

This is an experience-based interview question. The interviewer wants to
understand your practical exposure to building or maintaining an
observability stack, the tools you have used, and how you monitored
applications running in production.

### Answer

Yes. I have worked on implementing an observability stack for
Kubernetes-based applications.

My responsibilities included:

-   Setting up Prometheus to collect infrastructure and application
    metrics.
-   Creating Grafana dashboards for cluster and application monitoring.
-   Configuring Alertmanager for Slack and email notifications.
-   Collecting application logs using Fluent Bit and storing them in
    Loki.
-   Monitoring Kubernetes components using Node Exporter,
    kube-state-metrics, and cAdvisor.
-   Working with application teams to expose custom Prometheus metrics.
-   Troubleshooting production incidents using logs, metrics, and
    dashboards.

### Detailed explanation of the answer for readers' understanding

A typical observability architecture I worked with:

``` text
Applications
      │
      ├── Metrics (/metrics)
      ├── Logs
      │
      ▼
Fluent Bit            Prometheus
      │                    │
      ▼                    ▼
    Loki               Alertmanager
      │                    │
      └────────────┬────────┘
                   ▼
                Grafana
```

------------------------------------------------------------------------

## 1. Infrastructure Monitoring

I monitored Kubernetes worker nodes using **Node Exporter**.

Important metrics included:

-   CPU utilization
-   Memory usage
-   Disk utilization
-   Network traffic
-   Filesystem usage

These metrics helped detect resource bottlenecks before they affected
applications.

------------------------------------------------------------------------

## 2. Kubernetes Monitoring

Using **kube-state-metrics**, I monitored:

-   Pod status
-   Deployment availability
-   Replica counts
-   StatefulSets
-   DaemonSets
-   Node conditions

This helped identify unhealthy workloads and deployment failures.

------------------------------------------------------------------------

## 3. Container Monitoring

Using **cAdvisor**, I tracked:

-   Container CPU usage
-   Memory usage
-   Restart counts
-   Network traffic

These metrics helped diagnose container-level resource issues.

------------------------------------------------------------------------

## 4. Application Metrics

Applications exposed custom metrics through the `/metrics` endpoint.

Examples:

-   HTTP request count
-   Request latency
-   Error rate
-   Active requests

Prometheus scraped these metrics, and Grafana displayed them in
dashboards.

------------------------------------------------------------------------

## 5. Log Collection

Application logs were collected using **Fluent Bit**.

The logs were forwarded to **Loki**, where they could be searched in
Grafana.

Structured logging made troubleshooting much easier.

------------------------------------------------------------------------

## 6. Alerting

Alertmanager was configured with rules such as:

-   High CPU utilization
-   High memory usage
-   Pod restart spikes
-   Node not ready
-   High API latency
-   High HTTP 5xx error rate

Alerts were delivered to Slack and email for timely response.

------------------------------------------------------------------------

## 7. Incident Troubleshooting

When incidents occurred, I followed this workflow:

1.  Check Grafana dashboards for abnormal metrics.
2.  Review Prometheus metrics to identify affected components.
3.  Search application logs in Loki.
4.  Correlate metrics and logs to determine the root cause.
5.  Verify recovery after implementing the fix.

------------------------------------------------------------------------

## Typical interview answer

> Yes, I have worked on building and maintaining an observability stack
> in a Kubernetes environment. I used Prometheus to scrape
> infrastructure and application metrics, Grafana for dashboards,
> Alertmanager for notifications, Fluent Bit to collect logs, and Loki
> for centralized log storage. I also created dashboards, configured
> alerts, exposed custom application metrics, and used logs and metrics
> together to troubleshoot production issues.

### Best practices

-   Monitor infrastructure, Kubernetes, and applications together.
-   Use structured logging.
-   Expose custom business metrics.
-   Build actionable dashboards.
-   Configure meaningful alerts to reduce noise.

### Key takeaways

-   Observability combines metrics, logs, and alerting to understand
    system health.
-   Prometheus, Grafana, Fluent Bit, Loki, and Alertmanager form a
    common observability stack.
-   Dashboards and alerts should help identify issues quickly.
-   Correlating logs and metrics is essential for effective
    troubleshooting.