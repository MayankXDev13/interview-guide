## Prometheus Metrics Collected in a Production Environment

### Question

What kind of metrics do you scrape with Prometheus in your current
organization?

### Short explanation of the question

This question evaluates your practical experience with **Prometheus**.
Interviewers want to know which infrastructure, Kubernetes, and
application metrics you collect, why you collect them, and how they are
used for monitoring and alerting.

### Answer

In a typical Kubernetes-based production environment, Prometheus scrapes
metrics from multiple sources, including:

-   Kubernetes cluster components
-   Nodes
-   Containers and Pods
-   Applications
-   Databases
-   Ingress controllers
-   Message queues
-   Custom business metrics

These metrics are visualized in Grafana and used to trigger alerts
through Alertmanager.

### Detailed explanation of the answer for readers' understanding

A common Prometheus architecture looks like this:

``` text
Applications
      │
      ├── /metrics
      │
Node Exporter
kube-state-metrics
cAdvisor
Ingress Controller
Database Exporters
      │
      ▼
   Prometheus
      │
      ▼
    Grafana
      │
      ▼
 Alertmanager
```

------------------------------------------------------------------------

## 1. Node Metrics (Node Exporter)

These metrics monitor the health of Kubernetes worker nodes.

Common metrics:

-   CPU utilization
-   Memory usage
-   Disk usage
-   Disk I/O
-   Network traffic
-   Filesystem usage
-   Load average

Example metrics:

``` text
node_cpu_seconds_total
node_memory_MemAvailable_bytes
node_filesystem_avail_bytes
node_network_receive_bytes_total
```

------------------------------------------------------------------------

## 2. Kubernetes Metrics (kube-state-metrics)

These metrics provide information about Kubernetes resources.

Examples:

-   Pod status
-   Deployment replicas
-   StatefulSets
-   DaemonSets
-   Jobs
-   CronJobs
-   Node status
-   Persistent Volumes
-   Namespaces

Example metrics:

``` text
kube_pod_status_phase
kube_deployment_status_replicas_available
kube_node_status_condition
```

------------------------------------------------------------------------

## 3. Container Metrics (cAdvisor)

Container-level resource usage.

Examples:

-   CPU usage
-   Memory usage
-   Network usage
-   Container restarts

Example metrics:

``` text
container_cpu_usage_seconds_total
container_memory_usage_bytes
container_network_receive_bytes_total
```

------------------------------------------------------------------------

## 4. Application Metrics

Applications expose custom metrics through the `/metrics` endpoint.

Examples:

-   HTTP request count
-   Request latency
-   Error rate
-   Active users
-   API throughput

Example metrics:

``` text
http_requests_total
http_request_duration_seconds
http_requests_in_progress
```

------------------------------------------------------------------------

## 5. Database Metrics

Collected using exporters such as PostgreSQL Exporter or MySQL Exporter.

Examples:

-   Active connections
-   Query latency
-   Slow queries
-   Transactions
-   Cache hit ratio

------------------------------------------------------------------------

## 6. Ingress Metrics

Collected from NGINX Ingress or other ingress controllers.

Examples:

-   Request rate
-   HTTP status codes
-   Latency
-   TLS handshakes

------------------------------------------------------------------------

## 7. Business Metrics

Many organizations expose business-specific metrics.

Examples:

-   Orders processed
-   Payments completed
-   Failed logins
-   Queue length
-   Emails sent
-   Messages processed

These metrics help monitor business health in addition to
infrastructure.

------------------------------------------------------------------------

## Typical interview answer

> In my organization, Prometheus scrapes infrastructure metrics from
> Node Exporter, Kubernetes metrics from kube-state-metrics, container
> metrics from cAdvisor, and application metrics exposed through the
> `/metrics` endpoint. We also collect database and ingress metrics and
> visualize everything in Grafana. Alertmanager sends notifications
> based on thresholds for CPU, memory, pod health, request latency, and
> error rates.

### Best practices

-   Monitor infrastructure, Kubernetes, and applications together.
-   Expose meaningful custom metrics from applications.
-   Create Grafana dashboards for different teams.
-   Configure Alertmanager with actionable alerts.
-   Avoid collecting unnecessary high-cardinality metrics.

### Key takeaways

-   Prometheus collects metrics from multiple exporters and
    applications.
-   Common exporters include Node Exporter, kube-state-metrics,
    cAdvisor, and database exporters.
-   Infrastructure metrics alone are not enough; application and
    business metrics are equally important.
-   Metrics are used for dashboards, alerting, capacity planning, and
    troubleshooting.