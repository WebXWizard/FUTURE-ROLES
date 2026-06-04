# Phase 10: Security & Hardening (15 Days)

> Production security is paramount. Learn SSH hardening, Firewall configuration, SELinux, AppArmor, and fail2ban protection.

**Phase Duration**: 15 days

---

## 📋 What You'll Learn

```
├── SSH Hardening (Port, Keys, Root access)
├── Firewall (UFW, iptables, firewalld)
├── SELinux / AppArmor
├── Fail2Ban (Brute-force protection)
├── User Security
├── Permission Hardening
├── Audit Logging
├── Encryption
├── Certificate Management
├── Vulnerability Scanning
└── Security Best Practices
```

---

## 🗓️ संक्षिप्त गाइड

### **DAY 1-3: SSH Hardening**

```bash
# SSH config secure करना:
sudo nano /etc/ssh/sshd_config

# Key configurations:
Port 22                         # Change to non-standard
PermitRootLogin no             # Never allow root SSH
PasswordAuthentication no       # Keys only
PubkeyAuthentication yes        # Use keys
X11Forwarding no                # Disable X11
AllowUsers user1 user2          # Whitelist users
MaxAuthTries 3                  # Limit attempts
MaxSessions 5                   # Max sessions per user

# SSH keys setup:
ssh-keygen -t rsa -b 4096
ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
chmod 600 ~/.ssh/id_rsa         # Keys permission
chmod 644 ~/.ssh/id_rsa.pub
```

---

### **DAY 4-6: Firewall Configuration**

```bash
# UFW (Uncomplicated Firewall):
sudo ufw enable                 # Enable firewall
sudo ufw allow 22/tcp           # Allow SSH
sudo ufw allow 80/tcp           # Allow HTTP
sudo ufw allow 443/tcp          # Allow HTTPS
sudo ufw deny 23/tcp            # Deny Telnet
sudo ufw status
sudo ufw show added

# iptables (Advanced):
# Rules save permanently in /etc/iptables/rules.v4
sudo iptables -L -v -n          # List rules
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# firewalld:
sudo firewall-cmd --get-zones
sudo firewall-cmd --zone=public --add-service=http
sudo firewall-cmd --zone=public --add-port=8080/tcp
```

---

### **DAY 7-9: SELinux / AppArmor**

```bash
# SELinux (RedHat/CentOS):
# Mandatory Access Control - सभी को restrict करो, फिर allow करो

getenforce                      # Current mode
sudo setenforce Permissive      # Temporary
sudo setenforce Enforcing       # Enable

# AppArmor (Ubuntu/Debian):
# Similar but simpler

sudo systemctl status apparmor
sudo aa-status                  # Profile status
sudo aa-enforce /path/to/profile

# Common issues:
sudo grep DENIED /var/log/audit/audit.log | tail -20
sudo ausearch -m avc -ts recent
```

---

### **DAY 10-11: Fail2Ban & Protection**

```bash
# Fail2Ban (Brute-force protection):
sudo apt install fail2ban
sudo systemctl start fail2ban

# Configuration:
sudo nano /etc/fail2ban/jail.local
[DEFAULT]
bantime = 3600
findtime = 600
maxretry = 3

[sshd]
enabled = true
port = ssh

# Monitor:
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

---

### **DAY 12-13: User & Permission Security**

```bash
# Strong passwords:
sudo passwd username            # Change password
sudo chage -l username          # Password info
sudo chage -E -1 -m 0 -M 90 username  # Policy

# sudo security:
sudo visudo                     # Edit sudoers safely
# Add:
username ALL=(ALL) NOPASSWD: /usr/bin/restart

# User audit:
lastlog
failed_password_report() {
    grep "Failed password" /var/log/auth.log | \
    grep "$(date +%b\ %d)" | awk '{print $(NF-3)}' | \
    sort | uniq -c | sort -rn
}
```

---

### **DAY 14-15: Auditing & Certificates**

```bash
# Audit logging:
auditctl -l                     # List rules
auditctl -w /etc/shadow -p wa   # Monitor shadow file

# Certificates (SSL/TLS):
# Generate self-signed:
sudo openssl req -x509 -nodes -days 365 \
  -newkey rsa:2048 \
  -keyout /etc/ssl/private/server.key \
  -out /etc/ssl/certs/server.crt

# Check certificate:
openssl x509 -in cert.crt -text -noout
```

---

## 💡 Security Checklist

```
SSH:
☐ Root login disabled
☐ Password auth disabled (keys only)
☐ Non-standard port
☐ MaxAuthTries limited
☐ X11Forwarding disabled

Firewall:
☐ UFW/firewalld enabled
☐ Only needed ports open
☐ SSH rate limited

Users:
☐ Only necessary users
☐ Strong password policies
☐ sudo restricted

Logging:
☐ Audit logging enabled
☐ Logs monitored
☐ Fail2ban active

SELinux/AppArmor:
☐ Enabled and enforcing
☐ Policies in place
```

---

अगला: **Phase 11: Monitoring & Observability**
