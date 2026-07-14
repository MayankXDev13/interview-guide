## Question  
A user reports that the application is slow.  

**Task:**  
Explain how you would troubleshoot and identify the root cause.

### 📝 Short Explanation  
This tests your ability to troubleshoot performance issues across the **full stack** — from frontend to backend, database, infrastructure, and network.

## ✅ Answer  

### 🔍 Step-by-Step Investigation Approach:

---

### 🧭 1. **Clarify the Scope**
- Is the slowness reported by one user or many?
- Is it on specific pages, actions, or times of day?
- Which environment? (Production, staging, etc.)

> 🔹 This narrows down whether it’s **user-specific**, **global**, or **intermittent**.

---

### 🌐 2. **Check Frontend First**
- Use browser dev tools (`Network`, `Performance` tabs):
  - Slow JavaScript?
  - Large images or API calls?
  - High Time to First Byte (TTFB)?

> If TTFB is high, backend or infra may be the bottleneck.

---

### ⚙️ 3. **Backend API Performance**
- Check server response times (via APM tools like New Relic, Datadog, Prometheus).
- Identify slow endpoints or increased latency.
- Look for spikes in request durations.

---

### 💾 4. **Database Slowness**
- Are there slow queries or locking issues?
- Use `EXPLAIN` to optimize queries.
- Monitor CPU and disk I/O on DB server.
- Check for missing indexes.

---

### 📡 5. **Infrastructure & Resource Usage**
- Check CPU, memory, disk I/O using:
  ```bash
  top, htop, vmstat, iostat
  ```
- Check container or pod resource limits (Kubernetes).
- Scale up if usage is near limits (AutoScaling, HPA).

---

### 📈 6. **Monitor Logs & Alerts**
- Check application and server logs for errors or latency.
- Look for recent deployments or changes that may correlate with slowness.
- Verify alert dashboards.

---

### 🔄 7. **Caching & CDN Checks**
- Is the cache being missed or expired too frequently?
- Is your CDN serving static content properly?
- Validate that backend isn’t overloaded due to missing cache.

---

### 📶 8. **Network or DNS Latency**
- Run `ping`, `traceroute`, or `mtr` to check connectivity.
- Check if DNS lookup times are high.
- Consider edge latency if serving users globally.

---

### 🔄 9. **Rollbacks or Restarts**
- If slowness began after a new release:
  - Rollback the deployment.
  - Restart degraded pods or services.

---

### ✅ 10. **After Fix: Monitor & Prevent**
- Add better performance alerts (latency, CPU, DB).
- Set SLOs for key endpoints.
- Add automated profiling for slow endpoints.

---

> Summary:  
> App slowness can come from **frontend, backend, DB, infrastructure, or network**. Use a systematic layer-by-layer approach to isolate and fix the issue. Focus first on scope, then verify each component with logs, metrics, and tools.

---