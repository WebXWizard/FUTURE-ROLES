# Phase 06: Linux Networking (15 Days)

> Understand networking concepts necessary for production systems. Learn OSI Model, TCP/IP, DNS, DHCP, SSH, and networking troubleshooting.

**Phase Duration**: 15 days (one of the most important phases!)  
**Prerequisites**: Complete Phase 1-5

---

## 📋 What You'll Learn

```
├── OSI Model (7 layers)
├── TCP/IP Protocol Suite
├── IP Addressing और Subnetting
├── Network Commands (ifconfig, ip, netstat, ss, netcat)
├── DNS Configuration
├── DHCP Server Setup
├── SSH Security और Configuration
├── Network Troubleshooting
├── Firewall Basics (iptables)
├── Network Performance Tuning
├── Virtual Networking
└── Real-world Network Scenarios
```

---

## 🗓️ दिन-दर-दिन संक्षिप्त

### **DAY 1-2: OSI Model और TCP/IP**

```bash
# OSI Model की 7 layers:
# Layer 7: Application    (HTTP, FTP, SSH, DNS, SMTP)
# Layer 6: Presentation   (Encryption, Compression)
# Layer 5: Session        (Connection management)
# Layer 4: Transport      (TCP, UDP ports)
# Layer 3: Network        (IP addresses, routing)
# Layer 2: Data Link      (MAC addresses, switches)
# Layer 1: Physical       (Cables, signals)

# TCP/IP Model (practical):
# Application Layer  → HTTP, SSH, FTP
# Transport Layer    → TCP (reliable), UDP (fast)
# Internet Layer     → IP (routing)
# Link Layer         → Ethernet, WiFi
```

---

### **DAY 3-4: Network Commands**

```bash
# Interface info देखना:
ip addr show                    # All interfaces
ip link show                    # MAC addresses
ifconfig -a                     # Old method (deprecated)

# Routing:
ip route show                   # Current routes
route -n                        # Numeric format

# DNS:
nslookup example.com            # DNS lookup
dig example.com                 # Detailed DNS query
host example.com                # Simple DNS resolution

# Port listening:
netstat -tlnp                   # TCP ports listening
ss -tlnp                        # Modern method (netstat का replacement)
lsof -i :8080                   # Check specific port

# Traffic analysis:
ping google.com                 # Connectivity test
traceroute google.com           # Route path
mtr google.com                  # Real-time route analysis
```

---

### **DAY 5-7: IP Configuration**

```bash
# Static IP set करना:
sudo nano /etc/netplan/00-installer-config.yaml
# या
sudo ip addr add 192.168.1.100/24 dev eth0

# DHCP से IP लेना:
sudo dhclient eth0

# Interface up/down:
sudo ip link set eth0 up
sudo ip link set eth0 down

# DNS configuration:
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
```

---

### **DAY 8-10: SSH और Security**

```bash
# SSH key generate करना:
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa

# SSH config:
sudo nano /etc/ssh/sshd_config

# Key security settings:
Port 22
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

---

### **DAY 11-13: DNS और DHCP**

```bash
# DNS zone file format:
$TTL 86400
@  IN  SOA  ns1.example.com. admin.example.com. (
           2024053101  ; serial
           3600        ; refresh
           1800        ; retry
           604800      ; expire
           86400 )     ; minimum

# DHCP configuration:
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option domain-name-servers 8.8.8.8;
  option routers 192.168.1.1;
}
```

---

### **DAY 14-15: Network Troubleshooting**

```bash
# Connection debugging:
1. ping करो - network reachable है?
2. traceroute करो - path क्या है?
3. netstat/ss से ports देखो - listening है?
4. tcpdump से traffic देखो - क्या data flow हो रहा है?
5. DNS check करो - name resolution काम कर रही है?

# Common issues और solutions:
"No route to host"           → Firewall check करो, gateway setup करो
"Connection refused"         → Port listen नहीं कर रहा
"Temporary failure in name"  → DNS issue
"Network unreachable"        → Routing configuration problem
```

---

## 💡 Quick Labs

```bash
# Lab 1: Network interfaces
ip addr show
ip link show

# Lab 2: Routing
ip route show
traceroute google.com

# Lab 3: DNS
dig google.com
nslookup google.com

# Lab 4: Ports
ss -tlnp
netstat -tlnp

# Lab 5: SSH keys
ssh-keygen -t rsa -b 4096
ssh-copy-id user@host
```

---

## ✅ Interview Questions (संक्षेप में)

**Q: OSI Model क्या है?**
- 7 layers जो network communication को organize करती हैं

**Q: TCP vs UDP?**
- TCP = reliable, connection-oriented (HTTP, SSH)
- UDP = fast, connectionless (DNS, video streaming)

**Q: SSH क्यों secure है?**
- Encryption होता है, passwords नहीं भेजते, keys use करते हैं

**Q: DNS क्या करता है?**
- Domain names को IP addresses में convert करता है

---

अगले Phase में: **Storage Management** (LVM, RAID, Partitions)
