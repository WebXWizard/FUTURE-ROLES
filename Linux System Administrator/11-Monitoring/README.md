# Phase 11: Monitoring & Observability (10 Days)

> Learn production-grade monitoring tools. Understand Prometheus, Grafana, ELK Stack, and how to set up alerts for system health.

**Phase Duration**: 10 days

---

## 📋 What You'll Learn

```
├── Monitoring Basics
├── Prometheus (Time-series database)
├── Grafana (Dashboards)
├── ELK Stack (Elasticsearch, Logstash, Kibana)
├── Nagios/Icinga (Traditional monitoring)
├── Alerting
├── Custom Metrics
├── Health Checks
├── Log Aggregation
└── Performance Analysis
```

---

## 🗓️ गाइड

### **DAY 1-2: Monitoring Fundamentals**

```bash
# System metrics:
cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}')
memory=$(free | grep Mem | awk '{print ($3/$2)*100}')
disk=$(df / | tail -1 | awk '{print $5}')

# Create monitoring script:
#!/bin/bash
while true; do
    echo "$(date): CPU=$cpu_usage%, Memory=$memory%, Disk=$disk%"
    sleep 60
done
```

---

### **DAY 3-5: Prometheus Setup**

```bash
# Install Prometheus:
wget https://github.com/prometheus/prometheus/releases/download/v2.x/prometheus-2.x.linux-amd64.tar.gz
tar xzf prometheus-*.tar.gz
cd prometheus-*

# prometheus.yml configuration:
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'localhost'
    static_configs:
      - targets: ['localhost:9090']

# Start Prometheus:
./prometheus --config.file=prometheus.yml

# Access: http://localhost:9090
```

---

### **DAY 6-7: Grafana Dashboards**

```bash
# Install Grafana:
sudo apt install grafana-server
sudo systemctl start grafana-server

# Access: http://localhost:3000
# Default: admin/admin

# Create dashboard:
1. Add Prometheus datasource
2. Create panel
3. PromQL query: node_memory_MemFree_bytes
4. Set visualization type
5. Save dashboard
```

---

### **DAY 8-10: Logging & Alerting**

```bash
# ELK Stack (Elasticsearch, Logstash, Kibana):
# Elasticsearch: Store logs
# Logstash: Parse and process
# Kibana: Visualize

# Alerts (Prometheus):
alert_rules.yml:
- alert: HighCPU
  expr: node_cpu_usage > 80
  for: 5m
  annotations:
    summary: "High CPU"
    
# Notification:
- webhook_configs:
    - url: 'http://localhost:5001/'
```

---

## 💡 Monitoring Stack

```
Simple:           Standard:          Enterprise:
↓                 ↓                  ↓
Prometheus +      Prometheus +       ELK Stack +
Grafana           Grafana +          Prometheus +
                  AlertManager       Grafana +
                                     Custom tools
```

---

अगला: **Phase 12: Backup & Disaster Recovery**
