# Phase 05: Linux Services & Systemd (12 Days)

> Learn how background services work, how to start/stop them, and create your own services. This is the heart of production Linux.

**Phase Duration**: 12 days  
**Prerequisites**: Complete Phase 1-4  
**Why Important**: All system administrator tasks revolve around services

---

## 📋 What You'll Learn in This Phase

```
├── What are services?
├── What is systemd (new way vs old init.d)
├── Managing services with systemctl
├── How to create service files (.service)
├── Logging with journalctl
├── Boot targets and runlevels
├── Troubleshooting services
├── Creating custom services
├── Socket activation
└── Real-world service scenarios
```

---

## 🗓️ Day-by-Day Detailed Guide

### **DAY 1: Services Fundamentals**

#### 📖 सिद्धांत

**Service क्या है?**

```
एक program जो:
├── Background में चलता है (foreground नहीं)
├── Specific task करता है (web server, database, SSH आदि)
├── System के साथ start/stop होता है
├── Daemon कहलाता है (D से शुरू - "disk and execution monitor")
└── Logs maintain करता है
```

**Services की पहचान:**

```bash
# Process name के साथ 'd' लगाते हैं
apache2   → httpd        (web server daemon)
mysql     → mysqld       (database daemon)
openssh   → sshd         (SSH daemon)
nginx     → nginx        (web server daemon)
redis     → redis-server (cache daemon)
```

**Service का जीवन चक्र (Life Cycle):**

```
Boot
  ↓
systemd loads
  ↓
Services read करता है (/etc/systemd/system/)
  ↓
Startup dependencies execute
  ↓
Services start होती हैं
  ↓
Services चलती हैं (foreground या background)
  ↓
System shutdown होता है
  ↓
Services stop होती हैं gracefully
  ↓
System halt
```

---

#### 🧪 Lab 1.1: Running Services देखना

```bash
# Step 1: See all running services
systemctl list-units --type=service --state=running

# Step 2: Specific service देखो
systemctl status ssh
systemctl status apache2

# Step 3: Service की details
systemctl show ssh

# Step 4: Process ID से जानना
systemctl status -p (pidof sshd)

# Step 5: All services (running + stopped)
systemctl list-units --type=service --all
```

---

### **DAY 2: systemctl Command - Basics**

#### 📖 सिद्धांत

**systemctl क्या करता है:**

```bash
systemctl start service_name        # Start करो
systemctl stop service_name         # Stop करो
systemctl restart service_name      # Restart करो
systemctl reload service_name       # Config reload (gentle)
systemctl status service_name       # Status देखो
systemctl enable service_name       # Boot पर automatic start
systemctl disable service_name      # Boot पर automatic start OFF
systemctl is-active service_name    # Active है या नहीं?
systemctl is-enabled service_name   # Boot पर enable है या नहीं?
```

**Start vs Restart vs Reload:**

```
start:   Service को शुरुआत से शुरू करो (cold start)
         → पहले stop होगी, फिर start होगी
         → सभी connections close हो जाएंगे

restart: Service को gracefully restart करो
         → Stop करके फिर से start करो
         → Config reload होगी

reload:  केवल configuration reload करो
         → Service बंद नहीं होती
         → Active connections जारी रहते हैं
         → Apache, Nginx जैसे servers के लिए बेहतर है
```

---

#### 🧪 Lab 2.1: systemctl का उपयोग

```bash
# Step 1: SSH service की status देखो
systemctl status ssh

# Output:
# ● ssh.service - OpenBSD Secure Shell server
#    Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
#    Active: active (running) since Mon 2026-05-30 10:00:00 UTC; 5h ago

# Step 2: Service को stop करो
sudo systemctl stop ssh
systemctl status ssh
# Active होना चाहिए: inactive

# Step 3: फिर से start करो
sudo systemctl start ssh
systemctl status ssh
# Active होना चाहिए: active

# Step 4: Restart करो
sudo systemctl restart ssh
# Service दोबारा start होगी

# Step 5: Enable/Disable check करो
systemctl is-enabled ssh
# Output: enabled (boot पर automatically start होगी)

# Step 6: Disable करो
sudo systemctl disable ssh
systemctl is-enabled ssh
# Output: disabled

# Step 7: फिर से enable करो
sudo systemctl enable ssh

# Step 8: Multiple services
sudo systemctl start apache2 mysql redis-server
systemctl status apache2 mysql redis-server
```

---

### **DAY 3: Service Files Structure**

#### 📖 सिद्धांत

**Service File कहाँ होती है?**

```bash
/etc/systemd/system/            # System-wide services (सबसे महत्वपूर्ण)
/lib/systemd/system/            # Package-provided services
/run/systemd/system/            # Runtime services
~/.config/systemd/user/         # User-specific services
```

**Basic Service File Structure:**

```ini
[Unit]
Description=My Web Service
After=network.target

[Service]
Type=simple
User=www-data
ExecStart=/usr/bin/myservice
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

**हर section क्या करता है?**

```
[Unit]
├── Description: Service का विवरण
├── After: किन services के बाद start करो
├── Before: किससे पहले start करो
└── Requires: कौन-कौन सी services जरूरी हैं

[Service]
├── Type: कैसे run करेगा (simple, forking, notify, etc.)
├── User: किस user के रूप में चलेगा
├── ExecStart: कौन-कौन सी command run करेगी
├── ExecReload: Reload के समय क्या run करें
├── Restart: Fail होने पर क्या करें
├── RestartSec: कितने समय बाद restart करें
└── StandardOutput/StandardError: Logging कहाँ हो

[Install]
├── WantedBy: Enable करते समय कहाँ link बनाएं
├── RequiredBy: कौन services इसे need करती हैं
└── Alias: Alternative names
```

---

#### 🧪 Lab 3.1: Service Files देखना

```bash
# Step 1: SSH service की file देखो
cat /lib/systemd/system/ssh.service

# Output example:
# [Unit]
# Description=OpenBSD Secure Shell server
# After=network.target auditd.service
#
# [Service]
# Type=notify
# EnvironmentFile=-/etc/default/ssh
# ExecStartPre=/usr/sbin/sshd -t
# ExecStart=/usr/sbin/sshd -D $SSHD_OPTS
#
# [Install]
# WantedBy=multi-user.target

# Step 2: Apache service की file
cat /etc/systemd/system/apache2.service

# Step 3: सभी loaded services को देखो
systemctl list-unit-files --type=service
```

---

### **DAY 4: Custom Service बनाना**

#### 📖 सिद्धांत

**Custom service बनाने के Steps:**

```
1. Script बनाओ जो background में चले
2. Service file बनाओ (/etc/systemd/system/name.service)
3. systemctl daemon-reload करो (नई files को load करने के लिए)
4. systemctl enable करो (boot पर start के लिए)
5. systemctl start करो
6. systemctl status से verify करो
```

---

#### 🧪 Lab 4.1: अपनी खुद की Service बनाना

```bash
# Step 1: Script बनाओ जो background में चले
sudo cat > /usr/local/bin/myservice.sh << 'EOF'
#!/bin/bash
# Simple background service

LOG_FILE="/var/log/myservice.log"

echo "[$(date)] MyService started" >> $LOG_FILE

# Loop जो हर 10 seconds में करता कुछ
while true; do
    echo "[$(date)] MyService is running" >> $LOG_FILE
    sleep 10
done
EOF

sudo chmod +x /usr/local/bin/myservice.sh

# Step 2: Service file बनाओ
sudo cat > /etc/systemd/system/myservice.service << 'EOF'
[Unit]
Description=My Custom Service
After=network.target

[Service]
Type=simple
User=nobody
ExecStart=/usr/local/bin/myservice.sh
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
EOF

# Step 3: systemd को नई file से update करो
sudo systemctl daemon-reload

# Step 4: Service को enable करो (boot पर start होगी)
sudo systemctl enable myservice

# Step 5: Service को start करो
sudo systemctl start myservice

# Step 6: Status check करो
systemctl status myservice

# Step 7: Logs देखो
sudo tail -f /var/log/myservice.log

# Step 8: Service को stop करो
sudo systemctl stop myservice

# Step 9: Boot पर automatic start के लिए check करो
systemctl is-enabled myservice
# Output: enabled ✓

# Step 10: Service file को reload करते हुए restart करो
sudo systemctl daemon-reload
sudo systemctl restart myservice
```

---

### **DAY 5: journalctl - Logging System**

#### 📖 सिद्धांत

**journalctl क्या करता है?**

```
पुराना तरीका: /var/log/syslog, /var/log/auth.log अलग-अलग
नया तरीका (systemd): सभी logs एक जगह (journalctl)

फायदे:
├── Structured logging
├── सभी services के logs एक जगह
├── Timestamps के साथ
├── Priority levels के साथ
└── Real-time follow करो
```

**journalctl Commands:**

```bash
journalctl                          # सभी logs देखो
journalctl -f                       # Real-time follow (tail -f जैसे)
journalctl -u ssh                   # Specific service के logs
journalctl -u ssh --follow          # Follow करो
journalctl -n 50                    # Last 50 lines
journalctl --since "2 hours ago"    # Last 2 hours
journalctl -p err                   # सिर्फ errors
journalctl -p warning               # सिर्फ warnings
journalctl -x                       # Explanation के साथ
journalctl --boot                   # Current boot के logs
journalctl --boot=-1                # Previous boot के logs
journalctl -o json                  # JSON format में
```

---

#### 🧪 Lab 5.1: journalctl का उपयोग

```bash
# Step 1: सभी logs देखो
journalctl | head -20

# Step 2: SSH service के logs
journalctl -u ssh

# Step 3: SSH के logs, real-time follow करो
# (एक terminal में)
journalctl -u ssh -f

# (दूसरे terminal में)
# SSH को कुछ बार connect/disconnect करो
ssh localhost

# Step 4: Last 1 hour के logs
journalctl --since "1 hour ago"

# Step 5: Specific date और time के बीच
journalctl --since "2026-05-30 10:00:00" --until "2026-05-30 11:00:00"

# Step 6: Error priority के logs
journalctl -p err

# Step 7: Warning और ऊपर
journalctl -p warning

# Step 8: Multiple services
journalctl -u ssh -u apache2

# Step 9: Explanation के साथ
journalctl -xe

# Step 10: JSON में export करो
journalctl -u ssh -o json > ssh_logs.json
cat ssh_logs.json
```

---

### **DAY 6: Boot Targets & Runlevels**

#### 📖 सिद्धांत

**Boot Targets क्या हैं?**

```
पुराना Concept: Runlevels (0-6)
├── 0 = Halt
├── 1 = Single user mode
├── 3 = Multi-user (no GUI)
├── 5 = Multi-user with GUI
└── 6 = Reboot

नया systemd Concept: Boot Targets
├── poweroff.target      (0)
├── rescue.target        (1)
├── multi-user.target    (3)
├── graphical.target     (5)
└── reboot.target        (6)
```

**Default Target:**

```bash
systemctl get-default          # Current default target
systemctl set-default multi-user.target    # GUI के बिना
systemctl set-default graphical.target     # GUI के साथ
```

---

#### 🧪 Lab 6.1: Boot Targets

```bash
# Step 1: Current default target
systemctl get-default

# Step 2: Possible targets देखो
systemctl list-unit-files --type=target

# Step 3: Default को GUI के बिना set करो
sudo systemctl set-default multi-user.target

# Step 4: Verify करो
systemctl get-default

# Step 5: दूसरे target को तुरंत load करो (reboot के बिना)
sudo systemctl isolate multi-user.target

# Step 6: वापस GUI target में जाओ
sudo systemctl isolate graphical.target

# Step 7: Single-user mode में जाओ (recovery)
sudo systemctl rescue
# (यहाँ से 'exit' से निकलो)
```

---

### **DAY 7: Service Dependencies**

#### 📖 सिद्धांत

**Services के बीच की Dependency:**

```
Service A पहले run होनी चाहिए
  ↓
Service B उस पर depend करती है
  ↓
systemd automatic ordering करता है

Example:
├── Network service
│   ↓
├── SSH service (Network के बाद)
│   ↓
└── Web service (Network के बाद)
```

**Dependency Keywords:**

```
After=service.service        # इस service के बाद run करो
Before=service.service       # इस service से पहले run करो
Requires=service.service     # यह service जरूरी है
Wants=service.service        # यह service होनी तो बेहतर है पर जरूरी नहीं
PartOf=service.service       # इसका हिस्सा हूँ
```

---

#### 🧪 Lab 7.1: Dependencies को देखना

```bash
# Step 1: Service की dependency देखो
systemctl list-dependencies ssh

# Output:
# ssh.service
# ├── system.slice
# ├── network.target
# └── sshd.socket

# Step 2: Reverse dependency (किसका हिस्सा हूँ मैं)
systemctl list-dependencies ssh --reverse

# Step 3: Graphical target की dependencies
systemctl list-dependencies graphical.target

# Step 4: Custom service में dependency add करो
cat > /tmp/dependent.service << 'EOF'
[Unit]
Description=Dependent Service
After=ssh.service
Wants=ssh.service

[Service]
Type=simple
ExecStart=/bin/sleep infinity

[Install]
WantedBy=multi-user.target
EOF

sudo cp /tmp/dependent.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl list-dependencies dependent.service
```

---

### **DAY 8: Troubleshooting Services**

#### 📖 सिद्धांत

**Common Service Issues:**

```
1. Service fail हो रही है
   └── journalctl से logs देखो

2. Service boot पर start नहीं हो रही
   └── enabled है check करो, dependencies check करो

3. Service काम नहीं कर रही सही से
   └── restart करो, logs check करो, permissions check करो

4. Service port पर नहीं listen कर रही
   └── netstat से check करो, logs देखो

5. Multiple instances run हो रहे हैं
   └── systemctl की unique service ensure करो
```

---

#### 🧪 Lab 8.1: Troubleshooting Scenarios

```bash
# Scenario 1: Service fail हो रही है

# Problem:
systemctl status myservice
# Output: failed

# Diagnosis:
sudo journalctl -u myservice -n 20

# Solution: Logs के हिसाब से fix करो

# ================================

# Scenario 2: Service start नहीं हो रही

# Diagnosis:
systemctl status myservice
# Check: "Loaded" status क्या है?

# Solution:
sudo systemctl daemon-reload
sudo systemctl start myservice

# ================================

# Scenario 3: Port already in use

# Problem:
sudo systemctl start apache2
# Output: Address already in use

# Diagnosis:
sudo netstat -tlnp | grep 80
# या
sudo lsof -i :80

# Solution:
sudo killall apache2
sudo systemctl start apache2

# ================================

# Scenario 4: Service stuck in starting state

# Problem:
systemctl status myservice
# Output: activating (start) for 5 minutes...

# Solution:
sudo systemctl stop myservice
sudo systemctl reset-failed myservice
sudo systemctl start myservice
```

---

### **DAY 9: Socket Activation**

#### 📖 सिद्धांत

**Socket Activation क्या है?**

```
पुराना तरीका:
├── SSH service हमेशा चलती है (memory waste)
└── Request आने का इंतजार करती है

नया तरीका (Socket Activation):
├── ssh.socket सुनता है (lightweight)
├── Connection आता है
├── तब ssh.service start होती है
└── Memory efficient!
```

**SSH के साथ उदाहरण:**

```bash
systemctl status ssh.socket
systemctl status ssh.service

# दोनों के बीच relationship
systemctl list-sockets
```

---

#### 🧪 Lab 9.1: Socket Activation समझना

```bash
# Step 1: Socket-enabled services देखो
systemctl list-sockets

# Step 2: SSH socket और service देखो
systemctl status ssh.socket
systemctl status ssh.service

# Step 3: Socket को stop करो
sudo systemctl stop ssh.socket

# Step 4: अब SSH में connect करने का प्रयास करो
ssh localhost
# Connection refused होगा

# Step 5: Socket को फिर से start करो
sudo systemctl start ssh.socket

# Step 6: अब connect करो
ssh localhost
# काम करेगा, और service automatically start होगी
```

---

### **DAY 10: Unit Files in Depth**

#### 📖 सिद्धांत

**Advanced Service File Options:**

```ini
[Unit]
Description=Complex Service
Documentation=man:myservice(8)
After=network-online.target
Wants=network-online.target
StartLimitIntervalSec=60
StartLimitBurst=3

[Service]
Type=notify
User=myservice
Group=myservice
WorkingDirectory=/opt/myservice
ExecStartPre=/opt/myservice/check-deps.sh
ExecStart=/opt/myservice/start.sh
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/opt/myservice/stop.sh
StandardOutput=journal
StandardError=journal
SyslogIdentifier=myservice
Restart=on-failure
RestartSec=5
TimeoutStartSec=30
TimeoutStopSec=30
KillMode=mixed
Environment="SETTING1=value1"
EnvironmentFile=/etc/myservice/config

[Install]
WantedBy=multi-user.target
Alias=myservice
```

---

#### 🧪 Lab 10.1: Advanced Service File

```bash
# Step 1: Complex service file बनाओ
sudo cat > /etc/systemd/system/webserver.service << 'EOF'
[Unit]
Description=My Web Server
Documentation=http://example.com/docs
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=www-data
Group=www-data
WorkingDirectory=/var/www
ExecStartPre=/bin/mkdir -p /var/run/webserver
ExecStart=/usr/bin/python3 /var/www/server.py
ExecReload=/bin/kill -HUP $MAINPID
Restart=on-failure
RestartSec=10
StandardOutput=journal
StandardError=journal
Environment="DEBUG=false"
Environment="PORT=8000"

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl status webserver

# Step 2: Environment variables check करो
sudo systemctl show webserver -p Environment

# Step 3: Service के सभी properties
sudo systemctl show webserver
```

---

### **DAY 11: Real-World Service Scenarios**

#### Scenario 1: Database Service (MySQL/PostgreSQL)

```bash
# Service file:
cat /lib/systemd/system/mysql.service

# Key points:
# Type=forking           (background में जाता है)
# User=mysql             (specific user से चलता है)
# After=network.target   (network के बाद)
# Restart=on-abort       (fail होने पर restart)

# Management:
sudo systemctl restart mysql
sudo systemctl enable mysql
journalctl -u mysql -f
```

#### Scenario 2: Application Service (Node.js/Python)

```bash
# Service file:
sudo cat > /etc/systemd/system/myapp.service << 'EOF'
[Unit]
Description=My Node Application
After=network.target

[Service]
Type=simple
User=appuser
WorkingDirectory=/home/appuser/myapp
ExecStart=/usr/bin/node /home/appuser/myapp/server.js
Restart=always
RestartSec=10
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable myapp
sudo systemctl start myapp
sudo systemctl status myapp
```

#### Scenario 3: Monitoring Service (Prometheus)

```bash
# Service file:
sudo cat > /etc/systemd/system/prometheus.service << 'EOF'
[Unit]
Description=Prometheus Monitoring
After=network.target

[Service]
Type=simple
User=prometheus
ExecStart=/usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable prometheus
sudo systemctl start prometheus
```

---

#### 🧪 Lab 11.1: Production-like Service

```bash
# Complete service setup:

# Step 1: User बनाओ
sudo useradd -r -s /bin/false appservice

# Step 2: Application directory
sudo mkdir -p /opt/myapp
sudo chown appservice:appservice /opt/myapp

# Step 3: Application script
sudo cat > /opt/myapp/run.sh << 'EOF'
#!/bin/bash
while true; do
    echo "$(date): App running" >> /var/log/myapp.log
    sleep 5
done
EOF

sudo chmod +x /opt/myapp/run.sh

# Step 4: Service file
sudo cat > /etc/systemd/system/myapp.service << 'EOF'
[Unit]
Description=My Application Service
After=network.target syslog.target

[Service]
Type=simple
User=appservice
WorkingDirectory=/opt/myapp
ExecStart=/opt/myapp/run.sh
Restart=on-failure
RestartSec=10
StandardOutput=append:/var/log/myapp.log
StandardError=append:/var/log/myapp.log

[Install]
WantedBy=multi-user.target
EOF

# Step 5: Register और start करो
sudo systemctl daemon-reload
sudo systemctl enable myapp
sudo systemctl start myapp

# Step 6: Monitor करो
systemctl status myapp
journalctl -u myapp -f
sudo tail -f /var/log/myapp.log
```

---

### **DAY 12: Practice Assignments & Mini Project**

#### 📝 Assignment 1: Service Management

```bash
# Tasks:
# 1. SSH service को list करो (सभी details के साथ)
#    Answer: systemctl list-unit-files ssh*

# 2. Service status में क्या-क्या information दिखती है?
#    Answer: Active state, PID, Memory, CPU usage, logs last lines

# 3. Systemctl से कौन-कौन से commands हैं?
#    Answer: start, stop, restart, reload, enable, disable, status, etc.

# 4. Boot पर service automatic start करने के लिए क्या करते हैं?
#    Answer: systemctl enable servicename

# Save करो: ~/assignments/day12_services_q1.txt
```

#### 📝 Assignment 2: Service File Creation

```bash
# Requirement: एक backup service बनाओ जो:
# 1. Daily 2 AM पर backup लेगी
# 2. /data directory को /backups में copy करेगी
# 3. अगर fail हो तो auto-restart होगी
# 4. Logs journal में जाएंगे

# Steps:
# 1. Backup script बनाओ
# 2. Service file बनाओ
# 3. Timer file बनाओ (Day 12 - Advanced)
# 4. Enable और test करो

# Save files: ~/assignments/backup.service + backup.sh
```

#### 🎯 Mini Project: Service Management Suite

```bash
# Create ~/mini-projects/service-management-suite.sh

#!/bin/bash
# Service management utility

show_menu() {
    echo "=== Service Management Suite ==="
    echo "1. List all services"
    echo "2. Show service status"
    echo "3. Start service"
    echo "4. Stop service"
    echo "5. Restart service"
    echo "6. Enable service"
    echo "7. Disable service"
    echo "8. View service logs"
    echo "9. Exit"
    read -p "Choose option: " choice
}

while true; do
    show_menu
    case $choice in
        1) systemctl list-unit-files --type=service ;;
        2) read -p "Service name: " svc; systemctl status $svc ;;
        3) read -p "Service name: " svc; sudo systemctl start $svc ;;
        4) read -p "Service name: " svc; sudo systemctl stop $svc ;;
        5) read -p "Service name: " svc; sudo systemctl restart $svc ;;
        6) read -p "Service name: " svc; sudo systemctl enable $svc ;;
        7) read -p "Service name: " svc; sudo systemctl disable $svc ;;
        8) read -p "Service name: " svc; journalctl -u $svc -f ;;
        9) break ;;
    esac
done
```

---

## 📚 Summary: systemd Quick Reference

```
BASIC COMMANDS:
systemctl start service_name          # Start
systemctl stop service_name           # Stop
systemctl restart service_name        # Restart
systemctl reload service_name         # Reload config
systemctl reload-or-restart service   # Smart restart
systemctl enable service_name         # Auto-start on boot
systemctl disable service_name        # Disable auto-start
systemctl status service_name         # Current status
systemctl is-active service_name      # Is it running?
systemctl is-enabled service_name     # Is it enabled?

LISTING:
systemctl list-units --type=service   # All services
systemctl list-unit-files --type=service  # All service files
systemctl list-dependencies service   # What depends?
systemctl list-sockets                # All sockets

JOURNALCTL (LOGGING):
journalctl                            # All logs
journalctl -f                         # Follow (like tail -f)
journalctl -u service_name            # Specific service
journalctl -n 50                      # Last 50 lines
journalctl -p err                     # Errors only
journalctl --since "2 hours ago"      # Time filter

SERVICE FILE LOCATIONS:
/etc/systemd/system/           # User/admin services
/lib/systemd/system/           # Package services
/run/systemd/system/           # Runtime services
~/.config/systemd/user/        # User services

SERVICE FILE TEMPLATE:
[Unit]
Description=My Service
After=network.target

[Service]
Type=simple
User=username
ExecStart=/path/to/binary
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

---

## 💡 Interview Preparation

### Q1: systemd क्या है और पुराने init system से अलग क्या है?
**Answer**:
- systemd एक modern init system है जो services manage करता है
- पुराना system: init.d scripts, runlevels (0-6)
- नया system: unit files (.service), targets, dependencies, parallel startup
- फायदे: Faster boot, socket activation, journal logging, dependency resolution

### Q2: Service file का [Unit] section क्या करता है?
**Answer**:
- Service को describe करता है
- Dependencies specify करता है
- Other units के साथ ordering define करता है
- Key fields: Description, After, Before, Requires, Wants

### Q3: systemctl enable vs start में क्या फर्क है?
**Answer**:
- start: तुरंत शुरू करो (अभी, लेकिन reboot के बाद नहीं)
- enable: Boot पर automatic start करने के लिए link बनाओ
- दोनों चाहिए: enable (boot के लिए) + start (अभी के लिए)

### Q4: journalctl क्या है और /var/log से अलग क्या है?
**Answer**:
- journalctl: systemd का central logging system
- /var/log: पुराना traditional logging
- journalctl फायदे: structured, centralized, real-time, searchable by unit/priority/time

### Q5: Service fail हो रही है - troubleshoot कैसे करोगे?
**Answer**:
1. systemctl status service_name → status check करो
2. journalctl -u service_name → logs देखो
3. ExecStart की path verify करो (ls -la)
4. User permissions check करो
5. Dependencies resolve करो
6. Service file syntax check: systemd-analyze verify service.service

### Q6: SUID वाली executable को service से कैसे चलाते हो safely?
**Answer**:
- Service file में User specify करो
- SUID bit सेट न करो (dangerous)
- sudo via sudoers file use करो
- या dedicated user के साथ चलाओ जिसके पास specific commands के लिए sudo access हो

### Q7: Service के environment variables कैसे set करते हो?
**Answer**:
```bash
# Method 1: Service file में direct
Environment="VAR1=value1"
Environment="VAR2=value2"

# Method 2: External file से
EnvironmentFile=/etc/myservice/config
```

---

## ✅ Checklist: आपने क्या सीखा?

- [ ] Services क्या होती हैं समझ गए
- [ ] systemctl command सभी options के साथ सीख गए
- [ ] Service files कैसे बनाते हैं समझ गए
- [ ] Custom service बना सकते हो
- [ ] journalctl से logs देख सकते हो
- [ ] Boot targets को manage कर सकते हो
- [ ] Service dependencies समझ गए
- [ ] Troubleshooting कर सकते हो
- [ ] Real-world scenarios handle कर सकते हो
- [ ] Service security के बारे में सोच सकते हो

---

## 🚀 अगला Phase

**Phase 6: Linux Networking** (15 दिन)
- OSI Model
- TCP/IP Protocol Suite
- Network commands (ifconfig, ip, netstat, ss)
- DNS और DHCP
- SSH और remote access
- Network configuration
- Troubleshooting network issues

---

**Happy Learning! 🎓**

> **याद रखें**: systemd ने Linux system administration को revolutionize कर दिया है।
> अच्छे से समझो, तो हर production system में काम कर सकते हो।
