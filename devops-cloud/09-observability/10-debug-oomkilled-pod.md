## A Pod Crashes Randomly with OOMKilled. How Do You Identify and Fix It?

### Question

A pod crashes randomly with **OOMKilled**. How do you identify and fix
this?

### Short explanation of the question

This is a Kubernetes troubleshooting question. An **OOMKilled (Out Of
Memory Killed)** event means the Linux kernel terminated the container
because it exceeded its memory limit. The interviewer wants to
understand how you investigate the root cause and prevent it from
happening again.

### Answer

I follow a structured troubleshooting process:

1.  Confirm the pod was terminated due to **OOMKilled**.
2.  Check current and historical memory usage.
3.  Verify Kubernetes resource requests and limits.
4.  Investigate the application for memory leaks or excessive memory
    usage.
5.  Increase memory limits only if justified.
6.  Monitor the pod after the fix.

### Detailed explanation of the answer for readers' understanding

Typical investigation workflow:

``` text
Pod Restarts
      │
      ▼
kubectl describe pod
      │
      ▼
Reason = OOMKilled
      │
      ▼
Check Memory Metrics
      │
      ▼
Analyze Application
      │
      ▼
Adjust Resources or Fix Code
      │
      ▼
Monitor After Deployment
```

------------------------------------------------------------------------

## Step 1 --- Confirm the OOMKilled Event

Check the pod status:

``` bash
kubectl get pods
```

Describe the pod:

``` bash
kubectl describe pod <pod-name>
```

Example:

``` text
Last State:
  Terminated
  Reason: OOMKilled
  Exit Code: 137
```

Exit code **137** usually indicates the container was killed due to
memory exhaustion.

------------------------------------------------------------------------

## Step 2 --- Check Memory Usage

View current resource usage:

``` bash
kubectl top pod <pod-name>
```

For node usage:

``` bash
kubectl top node
```

Use Prometheus and Grafana to review:

-   Container memory usage
-   Memory working set
-   Memory limit
-   Restart count

Useful metrics:

``` text
container_memory_working_set_bytes
container_memory_usage_bytes
kube_pod_container_status_restarts_total
```

------------------------------------------------------------------------

## Step 3 --- Check Resource Requests and Limits

Review the deployment:

``` yaml
resources:
  requests:
    memory: "256Mi"
    cpu: "250m"
  limits:
    memory: "512Mi"
    cpu: "500m"
```

If the application regularly exceeds **512Mi**, Kubernetes terminates
the container.

------------------------------------------------------------------------

## Step 4 --- Investigate the Application

Possible causes:

-   Memory leak
-   Loading large files into memory
-   Unbounded caches
-   Too many concurrent requests
-   Inefficient queries or processing

Review application logs and use profiling tools if necessary.

------------------------------------------------------------------------

## Step 5 --- Apply the Fix

Depending on the root cause:

-   Optimize application memory usage.
-   Fix memory leaks.
-   Limit cache size.
-   Process data in smaller batches.
-   Increase memory limits if workload legitimately requires more
    memory.

Example:

``` yaml
resources:
  requests:
    memory: "512Mi"
  limits:
    memory: "1Gi"
```

------------------------------------------------------------------------

## Step 6 --- Verify After Deployment

After deploying the fix:

-   Monitor memory usage in Grafana.
-   Confirm restart count is no longer increasing.
-   Verify application latency and error rate.
-   Ensure the pod remains stable under load.

------------------------------------------------------------------------

## Common Root Causes

  Symptom                        Possible Cause
  ------------------------------ ----------------------------------
  Gradually increasing memory    Memory leak
  Crash during peak traffic      Memory limit too low
  Crash while processing files   Large in-memory objects
  Frequent restarts              Incorrect resource configuration
  High cache usage               Unbounded cache growth

------------------------------------------------------------------------

## Typical interview answer

> First, I confirm the pod was terminated with the reason `OOMKilled`
> using `kubectl describe pod`. Then I review memory usage using
> `kubectl top` and Grafana dashboards, verify resource requests and
> limits, inspect the application for memory leaks or inefficient memory
> usage, and apply the appropriate fix. After deployment, I monitor
> memory metrics and restart counts to ensure the issue is resolved.

### Best practices

-   Always define memory requests and limits.
-   Monitor container memory usage with Prometheus.
-   Investigate the application before simply increasing limits.
-   Perform load testing to validate memory requirements.
-   Configure alerts for high memory usage and repeated OOMKilled
    events.

### Key takeaways

-   OOMKilled means the container exceeded its memory limit.
-   Use `kubectl describe pod` to confirm the termination reason.
-   Combine Kubernetes events, Prometheus metrics, and application
    analysis to find the root cause.
-   Fix the application where possible; increase memory limits only when
    justified.