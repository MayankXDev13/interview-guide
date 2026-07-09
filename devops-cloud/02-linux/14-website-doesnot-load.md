## Question  
Your website is not loading.  

**Task:**  
Describe the step-by-step investigation process to identify and fix the issue.

### 📝 Short Explanation  
This is a high-pressure but common scenario that tests your ability to troubleshoot full-stack issues — from DNS and networking to web server and app code.

## ✅ Answer  

Start from **external checks** and move inward, layer by layer:

---

### 🧭 1. **Is the site down for everyone or just me?**
Use:
```bash
curl -I https://yourdomain.com
ping yourdomain.com
```
Or check with [https://downforeveryoneorjustme.com](https://downforeveryoneorjustme.com)

---

### 🌐 2. **DNS Resolution**
```bash
dig yourdomain.com
nslookup yourdomain.com
```
✅ Expect to get the correct IP.  
❌ No IP? Check DNS settings in Route53 (AWS) or other DNS provider.

---

### 🔁 3. **Is the domain routing to the correct server?**
Compare:
```bash
curl -v https://yourdomain.com
```
with server IP. If misrouted, verify **DNS records**, **load balancer config**, or **CDN rules**.

---

### 📡 4. **Network/Firewall Check**
- From your system:
```bash
telnet yourdomain.com 443
nc -zv yourdomain.com 80
```
- Check **security groups**, **firewalls**, or **NACLs** in cloud if ports are blocked.

---

### 🖥️ 5. **Is the Web Server running?**
SSH into your instance and check:

```bash
sudo systemctl status nginx
sudo systemctl status apache2
```

❌ If it’s down, restart:
```bash
sudo systemctl restart nginx
```

---

### 🧱 6. **Check Application Logs**
Look at logs for crash reports or errors:
- `/var/log/nginx/error.log`
- `/var/log/httpd/error_log`
- App logs: `app.log`, `stderr`, etc.

---

### 💾 7. **Check Disk/Memory/CPU**
```bash
df -h
top or htop
free -m
```
✅ Ensure the server isn't unresponsive due to resource exhaustion.

---

### 🔄 8. **Check Backend Services (DB, Cache, etc.)**
Your web app may be up, but failing due to:
- MySQL/Postgres down
- Redis/Memcached connection error
- App server crashes

---

### 🔐 9. **SSL Certificate Issues**
```bash
curl -Iv https://yourdomain.com
```
Look for:
```
SSL certificate problem
```

If expired, renew via Let’s Encrypt or your CA.

---

### 🧪 10. **Rollback or Revert**
If the issue started after a deploy:
- Rollback to the previous working build.
- Use:
```bash
kubectl rollout undo deployment your-deployment
```
or redeploy old version via your CI/CD.

---

### 🧠 Bonus Tip:
- Always check **uptime monitoring**, **alerting tools**, or **dashboards**.
- Build a **runbook** for your team for repeated scenarios.

> Summary:  
> Troubleshooting a website that won’t load requires a methodical approach — from DNS to server and app. Think layers: DNS → Network → Web Server → Application → Infrastructure → Dependencies.

---