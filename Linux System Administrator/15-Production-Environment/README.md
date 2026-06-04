# Phase 15: Production Operations (10 Days)

> Learn daily production tasks, incident handling, troubleshooting methodologies, and how to respond to system failures.

**Phase Duration**: 10 days

---

## 📋 What You'll Learn

```
├── On-Call Duties
├── Incident Response
├── Troubleshooting Methodologies
├── Performance Tuning
├── Capacity Planning
├── Change Management
├── Maintenance Windows
├── Log Analysis
├── Escalation Procedures
└── Documentation
```

---

## 🗓️ गाइड

### **DAY 1-2: Daily Tasks**

```bash
# Morning checks:
1. Service status check
   sudo systemctl status service_name
2. Disk usage
   df -h
3. Memory/CPU
   free -h; top -n 1
4. Error logs
   journalctl -p err --since "24 hours ago"
5. Alerts review
   Check monitoring dashboard

# Log rotation:
/etc/logrotate.d/custom:
/var/log/myapp.log {
    daily
    rotate 7
    compress
    delaycompress
    notifempty
    create 0640 www-data www-data
    sharedscripts
    postrotate
        systemctl reload myapp
    endscript
}
```

---

### **DAY 3-4: Incident Response**

```bash
# Incident categories:
1. Service Down (Critical)
   - Check service: systemctl status
   - Check logs: journalctl -u service -n 50
   - Restart: sudo systemctl restart service
   - If still down: escalate

2. High Load (Warning)
   - Check top processes: top
   - Check resources: free, df
   - Optimize or add resources

3. Disk Full (Critical)
   - Find large files: du -sh /path/*
   - Check logs: find /var/log -size +100M
   - Delete old logs or extend LVM

# Response template:
1. Assess severity
2. Page on-call if critical
3. Implement fix
4. Verify fix
5. Monitor
6. Post-mortem (if major incident)
```

---

### **DAY 5-6: Performance Tuning**

```bash
# Identify bottleneck:
1. CPU bound?   → optimize code, parallelize
2. Memory?      → cache, reduce heap size
3. Disk I/O?    → SSD, caching, optimize queries
4. Network?     → bandwidth upgrade, CDN

# Performance tools:
perf top                        # CPU profiling
iostat                          # Disk I/O
netstat                         # Network
iotop                           # Per-process I/O
```

---

### **DAY 7-8: Troubleshooting Methodology**

```bash
# Systematic approach:
1. What changed?
   - Recent deployments?
   - Configuration changes?
   - Hardware changes?
   - OS updates?

2. Gather data
   - Logs: journalctl, application logs
   - Metrics: CPU, memory, disk, network
   - System state: ps, netstat, lsof

3. Hypothesis
   - Based on data, what could be wrong?

4. Test hypothesis
   - Try fix in test environment
   - Monitor carefully

5. Implement & monitor
   - Apply fix
   - Watch for 24 hours minimum
   - Document

6. Post-mortem
   - What was root cause?
   - How to prevent?
   - Update runbooks
```

---

### **DAY 9-10: Runbooks & Documentation**

```bash
# Create runbooks for common issues:

## Runbook: Service Restart
1. SSH to server
2. sudo systemctl status service_name
3. If failed: sudo systemctl restart service_name
4. Verify: sudo systemctl status service_name
5. Check logs: journalctl -u service_name -n 50
6. Alert resolved or escalate

## Runbook: Disk Full
1. SSH to server
2. df -h (identify partition)
3. du -sh /* (find largest directories)
4. Either: delete files, rotate logs, or extend LVM
5. Verify: df -h

## On-call playbook:
1. Check alerting system
2. Assess severity (1-4 scale)
3. Engage appropriate team
4. Follow incident response process
5. Document everything
6. Post-incident review
```

---

## 💡 Escalation Matrix

```
Severity 1 (Critical):
  → Immediate page
  → Executive notification
  → Full team engaged

Severity 2 (High):
  → Page primary on-call
  → Senior engineer consultation
  → 1 hour resolution SLA

Severity 3 (Medium):
  → Next business day
  → Standard troubleshooting
  → 4 hour resolution SLA

Severity 4 (Low):
  → Backlog
  → Non-blocking
  → Best effort
```

---

अगला: **Phase 16: Interview Preparation**
