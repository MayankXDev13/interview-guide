## Difference Between Push-Based and Pull-Based Monitoring

### Question

What is the difference between push-based and pull-based monitoring?

### Short explanation of the question

This question tests your understanding of how monitoring systems collect
metrics. The two common approaches are **pull-based monitoring**, where
the monitoring server collects metrics, and **push-based monitoring**,
where applications or agents send metrics to a monitoring server.

### Answer

-   **Pull-based monitoring** means the monitoring system periodically
    **requests (scrapes)** metrics from applications or exporters.
-   **Push-based monitoring** means the application or agent **sends**
    metrics to the monitoring system without being asked.

Prometheus primarily uses the **pull model**, while systems such as
Graphite, InfluxDB (with Telegraf), StatsD, and cloud monitoring agents
commonly use the **push model**.

### Detailed explanation of the answer for readers' understanding

  -------------------------------------------------------------------------------
  Aspect             Pull-Based Monitoring          Push-Based Monitoring
  ------------------ ------------------------------ -----------------------------
  **Who initiates    Monitoring server              Application or agent
  communication?**                                  

  **Data flow**      Monitor → Target               Target → Monitor

  **Popular tools**  Prometheus                     StatsD, Graphite, Telegraf,
                                                    CloudWatch Agent

  **Discovery**      Easy with service discovery    Usually requires endpoint
                                                    configuration

  **Health           Missing scrape indicates       Harder to know if sender
  detection**        target issue                   silently fails
  -------------------------------------------------------------------------------

------------------------------------------------------------------------

## Pull-Based Monitoring

The monitoring server periodically scrapes metrics.

``` text
        Scrape
Prometheus ─────────► Application
                     (/metrics)
```

Example:

``` text
http://app:8080/metrics
```

Prometheus collects metrics every few seconds and stores them in its
time-series database.

### Advantages

-   Automatic service discovery
-   Easy target health monitoring
-   Simple configuration in Kubernetes
-   No agent logic required for sending metrics

### Disadvantages

-   Target must be reachable from Prometheus.
-   Not ideal for very short-lived jobs without additional components.

------------------------------------------------------------------------

## Push-Based Monitoring

Applications or agents send metrics to a monitoring system.

``` text
Application
      │
      ▼
 Monitoring Server
```

Examples include:

-   CloudWatch Agent
-   Telegraf
-   StatsD
-   Graphite

### Advantages

-   Useful when the monitoring server cannot reach targets.
-   Suitable for edge devices and restricted networks.
-   Good for short-lived batch jobs.

### Disadvantages

-   Harder to detect failed senders.
-   More complex endpoint management.

------------------------------------------------------------------------

## Prometheus Pushgateway

Although Prometheus uses a pull model, it supports short-lived jobs
through **Pushgateway**.

``` text
Batch Job
     │
 Push Metrics
     ▼
Pushgateway
     ▲
     │ Scrape
Prometheus
```

This is intended for batch jobs and should not replace normal scraping
for long-running services.

------------------------------------------------------------------------

## Kubernetes Example

In Kubernetes:

-   Applications expose a `/metrics` endpoint.
-   Prometheus discovers Pods and Services automatically.
-   Prometheus scrapes metrics at configured intervals.

This makes the pull model highly effective in dynamic environments.

------------------------------------------------------------------------

## Typical interview answer

> Pull-based monitoring is used by Prometheus, where the monitoring
> server periodically scrapes metrics from applications. Push-based
> monitoring sends metrics from the application or an agent to the
> monitoring system. Pull-based monitoring simplifies service discovery
> and health checks, while push-based monitoring is useful when targets
> are unreachable or for short-lived batch jobs.

### Best practices

-   Use pull-based monitoring for Kubernetes and long-running services.
-   Use Pushgateway only for short-lived batch jobs in Prometheus.
-   Configure service discovery to reduce manual maintenance.
-   Ensure scrape intervals and retention match monitoring requirements.

### Key takeaways

-   Pull: monitoring server collects metrics.
-   Push: applications or agents send metrics.
-   Prometheus primarily uses the pull model.
-   Pushgateway is a special solution for batch jobs in a Prometheus
    ecosystem.