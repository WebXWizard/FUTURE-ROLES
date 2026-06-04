# All Phases Overview & Quick Reference

## ✅ Completed Phases

### ✅ PHASE 1: Linux Fundamentals (5 Days)
**Topics Covered:**
- What is Linux? (History, advantages, use cases)
- Linux Architecture (User space, Kernel, Device drivers)
- Linux Distributions (Ubuntu, CentOS, RHEL, Debian)
- Installation (VirtualBox, Ubuntu setup)
- Boot Process (BIOS, GRUB, Kernel, Init, Target)
- Directory Structure (/bin, /etc, /home, /var, /tmp, etc)

**Labs Completed:**
- ✅ Lab 1.1: System Information Gathering
- ✅ Lab 1.2: Kernel Exploration
- ✅ Lab 1.3: Distribution Check
- ✅ Lab 1.4: VirtualBox Installation
- ✅ Lab 1.5: Boot Process Understanding
- ✅ Lab 1.6: Directory Structure Exploration

**Key Learnings:**
- What is Linux and how does it work
- Different distributions के बीच अंतर
- VM में Ubuntu successfully install किया
- File system structure को समझा

---

### ✅ PHASE 2: Linux Commands (20 Days)

**Section 1: Navigation Commands (Day 1-2)**
- `pwd` - Print working directory
- `cd` - Change directory
- `ls` - List directory contents (with all options)
- `mkdir` - Make directory

**Section 2: File Management (Day 3-4)**
- `touch` - Create/update files
- `cp` - Copy files (with -r, -p, -i, -v)
- `mv` - Move/rename files
- `rm` - Remove files (⚠️ carefully!)
- `cat` - View file contents
- `less/more` - View large files efficiently

**Section 3: Search Commands (Day 5-6)**
- `find` - Search by name, size, type, date, permissions
- `locate` - Quick database search
- `grep` - Search text content (regex support)

**Section 4: Text Processing (Day 7-8)**
- `sed` - Stream editor (replace, delete, modify)
- `awk` - Column/structured data processing
- `cut` - Extract specific columns

**Section 5: Compression (Day 9-10)**
- `tar` - Bundle files (with gzip/bzip2)
- `gzip/gunzip` - Compress individual files
- `zip/unzip` - Windows compatible compression

**Section 6: Package Management (Day 11-15)**
- `apt` - Ubuntu/Debian (apt update, apt install, apt remove)
- `yum/dnf` - CentOS/RHEL (yum install, yum remove)

**Section 7: Advanced Combinations (Day 16-20)**
- Piping और output redirection
- Command chaining
- Working with multiple files

**Key Takeaway:**
Linux में 80% काम इन basic commands से ही हो जाता है। हर command को thoroughly practice करो।

---

## 📋 Remaining Phases (Detailed Breakdown)

---

# PHASE 3: User & Group Management (8 Days)

## Topics to Cover

### Day 1: User Basics
- What is a user?
- User ID (UID), Group ID (GID)
- /etc/passwd structure
- /etc/shadow structure

### Day 2: Creating Users
- `useradd` command
- `adduser` (interactive)
- User home directory
- Default shell selection

### Day 3: Modifying Users
- `usermod` command
- Changing username, UID, groups
- Shell को change करना
- Account expiration

### Day 4: Deleting Users
- `userdel` command
- Home directory को handle करना
- Files का ownership

### Day 5: Group Management
- `groupadd`, `groupmod`, `groupdel`
- /etc/group structure
- Primary vs Secondary groups

### Day 6: Password Management
- `passwd` command
- Password aging (`chage`)
- /etc/login.defs
- Shadow files

### Day 7: Sudo Access
- `visudo` (safe way to edit sudoers)
- Sudo rules syntax
- User-specific sudo permissions
- %group sudoers entries

### Day 8: Hands-on Lab & Project
- 10 users create करो
- 5 groups create करो
- Sudo permissions configure करो
- User lifecycle को manage करो

## Interview Questions
1. UID 0 क्यों special है?
2. /etc/passwd में passwords नहीं होते - क्यों?
3. What happens to files when you remove a user?
4. Sudo को password के बिना कैसे setup करते हो?

---

# PHASE 4: File Permissions (10 Days)

## Topics to Cover

### Day 1-2: Basic Permissions
- `chmod` - Change permissions
- rwx bits (4,2,1)
- Octal notation (755, 644, 777)
- Symbolic notation (u+x, g-w, o=r)

### Day 3-4: Ownership
- `chown` - Change owner
- `chgrp` - Change group
- Recursive permissions (-R)
- Special cases

### Day 5-6: Advanced Permissions
- SUID (Set User ID)
- SGID (Set Group ID)
- Sticky Bit
- Real-world examples

### Day 7: ACLs (Access Control Lists)
- `getfacl`, `setfacl`
- Fine-grained permissions
- Default ACLs

### Day 8-9: Special Cases & Troubleshooting
- Permission denied errors
- Umask समझना
- Security implications
- Best practices

### Day 10: Lab & Project
- Permission system को master करो
- Security-critical directories को configure करो
- ACLs को implement करो

## Key Commands
```bash
chmod 755 file      # rwxr-xr-x
chmod u+x file      # User को execute permission add करो
chown user file     # Owner को change करो
chown user:group file  # Owner और group
chmod 4755 file     # SUID bit set करो
chmod 2755 dir      # SGID bit set करो
chmod 1777 /tmp     # Sticky bit set करो
```

---

# PHASE 5: Linux Services (12 Days)

## Topics to Cover

### Day 1: systemd Introduction
- What is systemd?
- Traditional init vs systemd
- Unit files
- Dependencies

### Day 2-3: systemctl Commands
- `systemctl start/stop/restart`
- `systemctl enable/disable`
- `systemctl status`
- `systemctl list-units`

### Day 4-5: Service Files
- Unit file syntax
- [Unit], [Service], [Install] sections
- Custom services create करना
- Service के साथ scripts

### Day 6: journalctl - Logging
- `journalctl` से logs देखना
- Filtering logs
- Real-time monitoring
- Log levels

### Day 7: Boot Targets
- Multi-user.target
- Graphical.target
- rescue.target
- `systemctl get-default`, `set-default`

### Day 8-9: Service Management
- Service को troubleshoot करना
- Failed services को fix करना
- Dependencies को manage करना

### Day 10-12: Hands-on Lab & Project
- Custom service create करो
- Service को troubleshoot करो
- Boot sequence को understand करो

## Key Commands
```bash
systemctl start nginx
systemctl enable nginx
systemctl status nginx
journalctl -u nginx
journalctl -f
journalctl -p err
systemctl list-units --type=service
```

---

# PHASE 6: Linux Networking (15 Days)

## Topics to Cover (बहुत महत्वपूर्ण Phase!)

### Day 1-2: OSI Model & TCP/IP
- OSI के 7 layers
- TCP/IP model
- IP addresses (IPv4, IPv6)
- Subnetting basics

### Day 3-4: Network Commands
- `ping` - Connectivity check
- `traceroute` - Path tracing
- `nslookup`, `dig` - DNS query
- `curl`, `wget` - Download/request

### Day 5-6: Network Information
- `ifconfig`, `ip addr show`
- `netstat`, `ss` - Network statistics
- `route` - Routing table
- `arp` - ARP table

### Day 7-8: DNS Configuration
- /etc/resolv.conf
- DNS servers configure करना
- Local DNS resolution

### Day 9-10: SSH (बहुत महत्वपूर्ण)
- What is SSH?
- SSH keys (public/private)
- ssh-keygen
- /etc/ssh/sshd_config
- SSH को harden करना

### Day 11: FTP, NFS, SMB
- FTP server setup
- NFS sharing
- Samba (Windows shares)

### Day 12-13: Firewall Basics
- iptables introduction
- firewalld (newer systems)
- Ports को open/close करना

### Day 14-15: Lab & Project
- Network को troubleshoot करो
- SSH keys को setup करो
- Multiple servers को network में configure करो

## Key Commands
```bash
ping google.com
traceroute google.com
nslookup google.com
dig google.com
curl https://api.example.com
wget https://example.com/file.zip
netstat -tulpn
ss -tulpn
route -n
ip addr show
ip route show
ssh-keygen -t rsa -b 4096
ssh -i key.pem user@host
```

---

# PHASE 7: Storage Management (12 Days)

## Topics to Cover (Admins के लिए बहुत critical!)

### Day 1-2: Disk Basics
- Hard disks कैसे काम करते हैं?
- What are partitions?
- MBR vs GPT

### Day 3-4: Partitioning Tools
- `fdisk` - MBR partitioning
- `gdisk` - GPT partitioning
- `parted` - Advanced tool

### Day 5: Filesystems
- ext4 (default Linux)
- XFS (high-performance)
- Btrfs (modern)
- Creating filesystems

### Day 6-7: Mounting
- `mount` command
- `/etc/fstab` configuration
- Persistent mounts
- Temporary mounts

### Day 8: LVM (Logical Volume Manager)
- PV (Physical Volumes)
- VG (Volume Groups)
- LV (Logical Volumes)
- Dynamic resizing

### Day 9: RAID
- RAID levels (0, 1, 5, 10)
- Redundancy समझना

### Day 10: Swap
- What is swap?
- Swap files vs Swap partitions
- Swap को configure करना

### Day 11-12: Lab & Project
- Disk को partition करो
- Filesystems create करो
- LVM को setup करो
- /etc/fstab को configure करो

---

# PHASE 8: Process Management (8 Days)

## Topics to Cover

### Day 1-2: ps Command
- `ps aux` - सभी processes
- `ps -ef` - पूरी information
- Process hierarchy (`ps -ef --forest`)

### Day 3: top और htop
- `top` - Real-time monitoring
- `htop` - Better interface
- Sorting करना
- Filtering करना

### Day 4: Process Signals
- `kill` command
- Signal numbers (SIGTERM, SIGKILL)
- `killall`, `pkill` - By name

### Day 5: Process Priority
- `nice` - New process के लिए
- `renice` - Running process के लिए
- Priority levels (-20 to +19)

### Day 6: Job Control
- Background (&) और foreground
- `jobs` command
- `fg`, `bg` commands
- `suspend` (Ctrl+Z)

### Day 7-8: Lab & Project
- Long-running processes को manage करो
- CPU-intensive tasks को handle करो
- Memory issues को diagnose करो

---

# PHASE 9: Shell Scripting (25 Days) - *यह सबसे important phase है!*

## Topics to Cover

### Weeks 1: Bash Basics
- What is a shell?
- Script को create और execute करना
- Shebang (`#!/bin/bash`)
- Comments

### Week 2: Variables
- String variables
- Numeric variables
- Array variables
- Variable expansion

### Week 3: Input/Output
- echo, printf
- read command
- Redirection (>, >>, <)
- Pipes (|)

### Week 4: Conditional Statements
- if, else, elif
- Test conditions ([ ], [[ ]], (( )))
- Logical operators (&&, ||, !)
- case statements

### Week 5: Loops
- for loops
- while loops
- until loops
- Loop control (break, continue)

### Week 6: Functions
- Function definition
- Parameters और return values
- Local vs Global variables
- Recursive functions

### Week 7: String Operations
- String manipulation
- Pattern matching
- Regular expressions (basic)

### Week 8-9: Scripting Projects
- **20 Beginner Scripts:**
  1. Welcome message script
  2. User input processing
  3. File operations
  4. System information
  5. Backup script
  ... (और 15 more)

- **20 Intermediate Scripts:**
  1. Log analysis script
  2. Server monitoring
  3. Database backup
  4. Deployment automation
  ... (और 16 more)

- **10 Real Production Scripts:**
  1. Application deployment
  2. Health check monitoring
  3. Auto-scaling triggers
  ... (और 7 more)

## Key Topics
```bash
# Variables
name="John"
age=25
files=(file1 file2 file3)

# Conditions
if [ $age -gt 18 ]; then
  echo "Adult"
fi

# Loops
for i in {1..10}; do
  echo $i
done

# Functions
function backup_files() {
  tar -czf backup.tar.gz $1
}
```

---

# PHASE 10: Security (15 Days)

## Topics to Cover

### Day 1-3: SSH Hardening
- SSH keys setup
- Disable password authentication
- Change default port
- Disable root login
- SSH config options

### Day 4-5: Firewall
- iptables basics
- firewalld (RHEL/CentOS)
- Opening/closing ports
- Connection tracking

### Day 6-7: SELinux / AppArmor
- SELinux (RHEL)
- AppArmor (Ubuntu/Debian)
- Contexts और labels
- Troubleshooting

### Day 8-9: Fail2Ban
- Brute-force protection
- IP banning
- Configuration

### Day 10-11: User & File Security
- Strong passwords
- File permissions review
- Sudo abuse prevention
- Account locking

### Day 12-13: System Hardening
- Unnecessary services disable करना
- Updates रखना
- Logging configure करना

### Day 14-15: Security Audit
- Security checklist बनाना
- Vulnerability scan करना
- Penetration testing basics

## Security Checklist
```
☑️ SSH को harden करना
☑️ Firewall को configure करना
☑️ SELinux को enable करना
☑️ Fail2Ban को setup करना
☑️ Sudo को properly configure करना
☑️ File permissions को audit करना
☑️ User accounts को review करना
☑️ Services को minimize करना
☑️ Logging को enable करना
☑️ Regular updates लेना
```

---

# PHASE 11: Monitoring (10 Days)

## Topics to Cover

### Day 1-2: System Monitoring Tools
- `top`, `htop` - CPU और RAM
- `iostat` - Disk I/O
- `vmstat` - Virtual memory
- `free` - Memory usage
- `df` - Disk space

### Day 3-4: Nagios
- Nagios installation
- Configuration
- Alerts setup करना

### Day 5-6: Prometheus & Grafana
- Metrics collection
- Dashboard बनाना
- Alerting

### Day 7-8: Log Analysis
- Log files को read करना
- ELK stack introduction
- Centralized logging

### Day 9-10: Monitoring Project
- Complete monitoring setup
- Multiple servers को monitor करना
- Alerts configure करना

---

# PHASE 12: Backup & Recovery (8 Days)

## Topics to Cover

### Day 1-2: Backup Strategies
- Incremental backups
- Differential backups
- Full backups
- Retention policies

### Day 3-4: Backup Tools
- `rsync` - Efficient file sync
- `tar` - Complete backups
- `dd` - Disk imaging

### Day 5: Disaster Recovery
- Recovery planning
- RPO/RTO
- Testing backups

### Day 6-7: Cloud Backups
- AWS S3 backups
- Azure blob storage
- Automated backups

### Day 8: Project
- Production backup setup
- Disaster recovery plan
- Regular restore testing

---

# PHASE 13: Cloud Basics (8 Days)

## Topics to Cover

### Day 1: Cloud Computing Introduction
- IaaS, PaaS, SaaS समझना
- Public, Private, Hybrid cloud

### Day 2-3: AWS EC2
- Instance types
- Launch करना
- Connect करना

### Day 4-5: AWS Storage & Networking
- EBS volumes
- S3 storage
- Security groups
- VPC basics

### Day 6-7: IAM (Identity Access Management)
- Users create करना
- Permissions assign करना
- Roles

### Day 8: Project
- Production-like EC2 setup
- Multiple instances को network में
- Database को integrate करना

---

# PHASE 14: Automation (10 Days)

## Topics to Cover

### Day 1-3: Cron Jobs
- Cron syntax समझना
- Regular backups schedule करना
- Log rotation

### Day 4-5: Bash Automation
- Complex scripts
- Error handling
- Logging

### Day 6-8: Ansible Basics
- Playbooks
- Inventory
- Tasks

### Day 9-10: Project
- Multi-server automation
- Configuration management
- Deployment automation

---

# PHASE 15: Production Environment (10 Days)

## Topics to Cover

### Day 1-2: Daily Admin Tasks
- Backups checking करना
- Performance monitoring
- Security updates

### Day 3-4: Incident Response
- Issue identification
- Root cause analysis
- Resolution

### Day 5-6: Capacity Planning
- Growth forecasting
- Resource optimization
- Cost management

### Day 7-8: Change Management
- Change requests
- Testing
- Rollback plans

### Day 9-10: Documentation
- Runbooks बनाना
- Procedures document करना
- Knowledge base maintain करना

---

# PHASE 16: Interview Preparation (15 Days)

## 200+ Interview Questions

### Categories:
- **Linux Fundamentals** (20 questions)
- **Commands** (30 questions)
- **User Management** (20 questions)
- **File Permissions** (20 questions)
- **Networking** (25 questions)
- **Storage** (20 questions)
- **Scripting** (30 questions)
- **Security** (20 questions)
- **Performance** (15 questions)
- **Scenario-based** (50 questions)

### Scenario-based Example:
```
Q: आपका web server अचानक down हो गया। 
   What steps will you take for troubleshooting?

A: 
1. Server को check करो - SSH connect कर सकते हो?
2. systemctl status nginx
3. Logs को check करो - journalctl -u nginx -n 50
4. Disk space check करो - df -h
5. CPU/Memory check करो - top
6. Network check करो - netstat -tulpn | grep nginx
7. Configuration issues - nginx -t
8. Restart करो - systemctl restart nginx
```

---

# PHASE 17: Portfolio Projects (20 Days)

## Beginner Projects (10)
1. Personal backup system
2. System health monitor
3. Log analyzer
4. User management utility
5. File permissions audit tool
6. Cron job manager
7. DNS query tool
8. Network diagnostics suite
9. System information dashboard
10. Disk space analyzer

## Intermediate Projects (10)
1. Multi-server deployment tool
2. Automated configuration management
3. Security audit framework
4. Performance optimization suite
5. Disaster recovery system
6. Centralized monitoring solution
7. Container orchestration helper
8. Database backup manager
9. SSL certificate automation
10. CI/CD pipeline automation

## Advanced Projects (10)
1. Infrastructure automation platform
2. Cloud resource manager
3. Security hardening framework
4. Performance tuning engine
5. Capacity planning tool
6. Cost optimization system
7. Chaos engineering platform
8. Load balancer controller
9. Kubernetes operator
10. Full-stack DevOps platform

---

# PHASE 18: Job Preparation (7 Days)

## Resume Building
- Linux skills को highlight करना
- Projects को showcase करना
- Achievements को quantify करना

## LinkedIn Optimization
- Profile complete करना
- Linux admin communities join करना
- Thought leadership articles

## GitHub Portfolio
- Scripts को push करना
- Project repositories
- Documentation maintain करना
- README files quality

## Job Search Strategy
- Target companies research करना
- LinkedIn job search tips
- Interview preparation
- Negotiation strategy

---

## 🎯 Overall Learning Checklist

### Phase-wise Completion Status

```
PHASE 1: Linux Fundamentals          ✅ COMPLETE
PHASE 2: Linux Commands              ✅ COMPLETE  
PHASE 3: User & Group Management     ⏳ START NOW
PHASE 4: File Permissions            ⏳ (7 days)
PHASE 5: Linux Services              ⏳ (12 days)
PHASE 6: Linux Networking            ⏳ (15 days)
PHASE 7: Storage Management          ⏳ (12 days)
PHASE 8: Process Management          ⏳ (8 days)
PHASE 9: Shell Scripting             ⏳ (25 days) ⭐ CRITICAL
PHASE 10: Security                   ⏳ (15 days)
PHASE 11: Monitoring                 ⏳ (10 days)
PHASE 12: Backup & Recovery          ⏳ (8 days)
PHASE 13: Cloud Basics               ⏳ (8 days)
PHASE 14: Automation                 ⏳ (10 days)
PHASE 15: Production Environment     ⏳ (10 days)
PHASE 16: Interview Preparation      ⏳ (15 days)
PHASE 17: Portfolio Projects         ⏳ (20 days)
PHASE 18: Job Preparation            ⏳ (7 days)
```

---

## 📚 Additional Resources

### Books
- "The Linux Command Line" - William Shotts
- "Linux Administration Handbook" - Evi Nemeth
- "How Linux Works" - Brian Ward
- "The Practice of System and Network Administration" - Limoncelli

### Online Platforms
- Linux Academy
- Udemy
- Coursera
- Pluralsight
- Linux Foundation courses

### Community
- Reddit: r/linux, r/linuxadmin
- Stack Overflow
- Linux forums
- Ubuntu community

### Tools to Master
- vim/nano - Text editors
- tmux - Terminal multiplexer
- git - Version control
- ssh - Remote access
- docker - Containerization
- ansible - Configuration management

---

## 💡 Success Tips

### दैनिक Habits बनाओ
```
✅ रोज 4-5 घंटे study करो
✅ हर command को manually type करो
✅ नोट्स लें
✅ Labs को complete करो
✅ Advanced problems को solve करो
✅ Real servers पर practice करो
```

### Learn from mistakes
```
✅ Errors को read करो समझ में आए
✅ Logs को analyze करो
✅ Google अपना best friend है
✅ Community से सवाल पूछो
✅ Practice, practice, practice
```

### Progress को Track करो
```
✅ Daily tasks को mark करो
✅ Weekly reviews लो
✅ Completed assignments को save करो
✅ Interview Q&A को prepare करो
✅ Projects को document करो
```

---

**You're ready to start now!**

**Next Step: Go to Phase 3 - User & Group Management**

**आपका लक्ष्य: 6 महीने में job-ready Linux Admin बनना! 🚀**

