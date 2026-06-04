# PHASE 1: Linux Fundamentals - Complete Guide

## 📚 विषय सूची (Table of Contents)

1. What is Linux?
2. Linux Architecture
3. Linux Distributions
4. Installing Linux
5. Virtual Machines (VirtualBox)
6. Linux Boot Process
7. Linux Directory Structure

---

# 1️⃣ What is Linux? (Linux क्या है?)

## 🎓 Theory (सिद्धांत)

### Linux की परिभाषा
Linux एक **Free and Open-Source Operating System** है जो Unix पर आधारित है।

```
Linux = Kernel + GNU Utilities + Package Manager + Shell
```

### Linux का इतिहास
- **1991**: Linus Torvalds ने Linux kernel बनाया
- **1992**: Linux GPL के अंतर्गत आया
- **1993**: GNU Linux का पहला version
- **आज**: सबसे popular OS है servers, clouds, smartphones में

### Linux vs Windows vs macOS

| विशेषता | Linux | Windows | macOS |
|---------|-------|---------|-------|
| Open Source | ✅ हाँ | ❌ नहीं | ❌ नहीं |
| Cost | ✅ मुफ्त | ❌ महंगा | ❌ महंगा |
| Security | ✅ ज्यादा | ⚠️ मध्यम | ✅ अच्छा |
| Flexibility | ✅ उच्च | ⚠️ सीमित | ⚠️ सीमित |
| Server Use | ✅ 96% | ⚠️ 1% | ❌ 0.5% |

### Linux के लाभ (Advantages)

```
✅ Free - कोई licensing cost नहीं
✅ Open Source - source code publicly available
✅ Secure - strong security features
✅ Stable - months-years तक uptime
✅ Portable - desktop, server, mobile, IoT सब पर चलता है
✅ Multi-user - multiple users एक साथ काम कर सकते हैं
✅ Multi-tasking - multiple programs एक साथ चल सकते हैं
✅ Community Support - बहुत बड़ा community
```

### Linux का उपयोग कहां होता है?

```
🖥️ Web Servers
   - Apache, Nginx, IIS पर चलते हैं Linux पर

📊 Data Centers
   - Facebook, Google, Amazon सब Linux use करते हैं

☁️ Cloud Platforms
   - AWS, Azure, GCP सब Linux based हैं

📱 Mobile Devices
   - Android Linux पर आधारित है

🔧 IoT Devices
   - Smart TV, Routers, Cameras आदि

🎮 Gaming
   - PlayStation 4, 5 Linux पर आधारित हैं
```

---

## 💡 Real-world Example

### Example: Facebook का Infrastructure

```
Facebook के servers:
├── Web Servers (हजारों) - Linux पर
├── Database Servers - Linux पर
├── Cache Servers (Memcached) - Linux पर
├── Message Queues (Kafka) - Linux पर
└── Load Balancers - Linux पर

अगर कोई user भारत से photo upload करता है:
1. Request Linux Web Server को जाती है
2. Linux Database Server में store होती है
3. Linux Cache Server उसे fast deliver करता है
4. सब कुछ Linux admin manage करता है
```

---

## 🧪 Hands-on Lab 1.1: Linux System को समझना

### Lab Objective
अपने Linux system को explore करना और basic जानकारी निकालना

### Step-by-Step Guide

```bash
# Step 1: OS का नाम और version check करें
cat /etc/os-release

# Output होगा कुछ इस तरह:
# NAME="Ubuntu"
# VERSION="22.04 LTS"
# PRETTY_NAME="Ubuntu 22.04.1 LTS"

# Step 2: Kernel का version check करें
uname -a

# Output:
# Linux hostname 5.15.0-56-generic #62-Ubuntu SMP Tue Nov 22 21:24:20 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux

# Step 3: System की specifications देखें
uname -r  # Kernel release
uname -m  # Machine hardware name (x86_64, i686, etc.)

# Step 4: Hostname check करें
hostname

# Step 5: Kernel की विस्तृत जानकारी
cat /proc/version

# Step 6: System को कितना समय से चला है (uptime)
uptime

# Output:
# 10:30:45 up 5 days, 3:25, 2 users, load average: 0.05, 0.08, 0.10
```

### Lab Output को Understand करना

```
❓ "10:30:45 up 5 days, 3:25, 2 users, load average: 0.05, 0.08, 0.10"

✅ 10:30:45 = Current system time
✅ up 5 days, 3:25 = System 5 दिन और 3 घंटे 25 मिनट से चल रहा है
✅ 2 users = 2 users logged in हैं
✅ load average: 0.05, 0.08, 0.10
   = Last 1, 5, 15 minutes में average load
```

---

## ❓ Interview Questions

### Q1: Linux क्या है?
**Answer:**
Linux एक free और open-source Unix-like operating system है जिसे Linus Torvalds ने 1991 में बनाया था। यह kernel + GNU utilities का combination है जो multi-user, multi-tasking, portable और secure है।

### Q2: Linux, Unix, और Windows में क्या अंतर है?
**Answer:**
```
Linux:
- Free and Open Source
- Unix based
- Highly secure
- उपयोग: Servers, Cloud, IoT

Unix:
- Proprietary
- Expensive
- Enterprise systems में
- Legacy systems

Windows:
- Proprietary
- Expensive
- User-friendly GUI
- Desktop और Office systems में
```

### Q3: Linux के क्या लाभ हैं?
**Answer:** (बताए गए advantages को याद रखें)

### Q4: Linux कहां उपयोग होता है?
**Answer:** (बताए गए use cases को याद रखें)

### Q5: Linux 96% servers पर क्यों चलता है?
**Answer:**
- Cost-effective (free)
- Stable और reliable
- Excellent security
- Scalable
- Good performance
- Open source
- Large community support

---

## 🔧 Troubleshooting Scenario

### Scenario 1: "Linux version check नहीं हो रहा"

```bash
❌ Problem:
$ lsb_release -a
Command 'lsb_release' not found

✅ Solution:
# कुछ minimal Linux systems में यह utility नहीं होती
# Use करें ये alternatives:
cat /etc/os-release
cat /etc/lsb-release
uname -a
```

---

## 📝 Assignments

### Assignment 1: OS Information Document
अपने Linux system की निम्नलिखित जानकारी निकालें और एक text file में document करें:

```bash
# सभी जानकारी निकालें:
1. OS Name और Version
2. Kernel Version
3. System Uptime
4. Hostname
5. Architecture (32-bit या 64-bit)
6. Processor Information
7. Total RAM
8. Disk Size

# Output को save करें:
$ uname -a > my-system-info.txt
$ cat /etc/os-release >> my-system-info.txt
$ uptime >> my-system-info.txt
```

### Assignment 2: Linux के 5 Use Cases
अपने आसपास के 5 Linux systems को ढूंढें:
1. _________________
2. _________________
3. _________________
4. _________________
5. _________________

### Assignment 3: Comparison Chart
Windows और Linux को compare करते हुए एक chart बनाएं।

---

## 🎯 Mini Project 1: "My Linux Journey Document"

### Project Goal
एक document बनाएं जो आपके Linux learning journey को track करे।

### Project Steps

```markdown
# My Linux Journey

## Week 1: Fundamentals

### Day 1: Introduction
- Learned: Linux definition, history, advantages
- Key Points:
  - Linux is free and open source
  - Used in 96% of web servers
  - Created by Linus Torvalds in 1991
  
### Day 2: Distribution Understanding
- Studied: Different Linux distributions
- Differences: Ubuntu vs CentOS vs RHEL
- Key Points:
  ...

### Lab Completed
- ✅ Lab 1.1: System Information Gathering

### Questions to Remember
1. What is Linux?
2. Why is Linux so popular?
3. ...

### Resources Used
- Linux Foundation
- Official Documentation
- Man Pages
- Community Forums

### Progress
- Completed: 20%
- Next: Linux Architecture
```

---

# 2️⃣ Linux Architecture (Linux की संरचना)

## 🎓 Theory

### Linux Architecture Diagram

```
┌─────────────────────────────────────────────────────┐
│                  USER SPACE (USER LEVEL)             │
│  ┌────────────────┬──────────────┬─────────────────┐ │
│  │   Applications │    Shells    │   GNU Utilities │ │
│  │  (Firefox,     │  (bash, sh)  │   (ls, cat,    │ │
│  │   Browsers,    │              │    grep, etc)  │ │
│  │   Editors)     │              │                 │ │
│  └────────────────┴──────────────┴─────────────────┘ │
│  ┌──────────────────────────────────────────────────┐ │
│  │         System Libraries (libc, libm, etc)       │ │
│  │        (Applications इन्हें call करते हैं)         │ │
│  └──────────────────────────────────────────────────┘ │
│  ┌──────────────────────────────────────────────────┐ │
│  │              System Calls Interface              │ │
│  │   (read, write, fork, open, close, exec)        │ │
│  └──────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────┘
                          ▲
                          │ System Call
                          ▼
┌─────────────────────────────────────────────────────┐
│                 KERNEL SPACE (KERNEL LEVEL)         │
│  ┌──────────────────────────────────────────────────┐ │
│  │         Kernel (Core of Linux OS)                │ │
│  │  • Process Management                            │ │
│  │  • Memory Management                             │ │
│  │  • File System Management                        │ │
│  │  • Device Management                             │ │
│  │  • Networking                                    │ │
│  │  • Interrupt Handling                            │ │
│  └──────────────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────────────┐  │
│  │   Device Drivers                                 │  │
│  │   (Hardware को Control करते हैं)                  │  │
│  │  • Disk Drivers                                  │  │
│  │  • Network Drivers                               │  │
│  │  • Graphics Drivers                              │  │
│  │  • USB Drivers                                   │  │
│  └─────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────┘
                          ▲
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│                  HARDWARE LEVEL                      │
│  • CPU (Processor)                                  │
│  • RAM (Memory)                                     │
│  • Hard Disk                                        │
│  • Network Interface                                │
│  • USB Ports                                        │
│  • Keyboard, Mouse                                  │
└─────────────────────────────────────────────────────┘
```

### Architecture के 4 Main Components

#### 1. **User Space (यूजर स्पेस)**
```
जो आप और दूसरे programs चलाते हैं:
├── Applications (Firefox, Text Editor, etc)
├── Shells (bash, zsh, etc)
├── GNU Utilities (ls, cat, grep, etc)
└── Libraries (libc, libm, etc)

यह सब अलग-अलग "processes" हैं।
```

#### 2. **Kernel (कर्नल)**
```
Linux का दिल - सब कुछ control करता है:
├── Process Management - कौन सी process कब run करे
├── Memory Management - RAM को allocate करना
├── File System - Files को store और access करना
├── Device Management - Hardware को control करना
├── Networking - Internet communication
└── Interrupt Handling - Hardware signals को handle करना
```

#### 3. **Device Drivers (ड्राइवर्स)**
```
Hardware और Kernel के बीच communicator:
├── Disk Drivers - Hard disk को पढ़ते-लिखते हैं
├── Network Drivers - Internet connection
├── Graphics Drivers - Display
└── USB Drivers - USB devices को connect करते हैं
```

#### 4. **Hardware (हार्डवेयर)**
```
भौतिक devices:
├── CPU - Processor
├── RAM - Main memory
├── Hard Disk - Storage
├── Network Card - Internet
├── Keyboard, Mouse - Input devices
└── Monitor - Output device
```

### Flow: User से Hardware तक

```
User करता है: $ ls

Step 1: Shell (bash) को command मिलती है
        ls

Step 2: Shell को "ls" का program पता है
        /usr/bin/ls को execute करता है

Step 3: Program (ls) "read directory" के लिए
        System Call करता है

Step 4: Kernel यह System Call receive करता है
        और अपना काम करता है

Step 5: Kernel Device Driver को कहता है:
        "Hard disk से data निकालो"

Step 6: Device Driver Hardware को control करता है
        Hard disk से data निकालता है

Step 7: Kernel data को Program को देता है

Step 8: Program को data मिलता है
        Screen पर print करता है

Output: 
Desktop  Documents  Downloads  Music  Pictures
```

---

## 💡 Real-world Example

### Example: File को खोलना और पढ़ना

```bash
$ cat /home/user/data.txt

क्या होता है पर्दे के पीछे:

1. Shell: "cat" command को parse करता है
   
2. /usr/bin/cat program start होता है
   
3. cat program: "मुझे /home/user/data.txt की जरूरत है"
   System Call करता है: open("/home/user/data.txt")
   
4. Kernel:
   - File descriptor check करता है
   - Permission check करता है (क्या user को read permission है?)
   - File को search करता है
   - File का inode निकालता है
   
5. File System Layer:
   - inode से actual block address निकालता है
   - Block addresses note करता है
   
6. Device Driver:
   - Hard disk को कहता है: "इन block addresses से data निकालो"
   - Hard disk से data fetch करता है
   
7. Kernel:
   - Data को user space में copy करता है
   - File descriptor return करता है
   
8. cat program:
   - Data को read करता है
   - STDOUT (screen) पर print करता है
   
Final Output: File का content screen पर दिखता है
```

---

## 🧪 Hands-on Lab 1.2: Kernel को समझना

### Lab: Kernel Information Explore करना

```bash
# Step 1: Kernel की basic information
uname -a

# Step 2: Kernel की version
uname -r

# Step 3: Kernel के built-in modules
lsmod | head -20

# Output देखें (Loaded kernel modules)

# Step 4: System calls count करें
man 2 intro | head -20

# Step 5: Kernel के log देखें
dmesg | head -20

# यह दिखाता है कि kernel boot के समय क्या-क्या load कर रहा था

# Step 6: Process management को देखें
ps aux | head -10

# System में कौन-कौन सी processes चल रही हैं
```

---

## ❓ Interview Questions for Architecture

### Q1: Linux Architecture में Kernel क्या role play करता है?
**Answer:**
Kernel Linux का central component है जो:
- Hardware और Software के बीच interface प्रदान करता है
- System resources (CPU, RAM, Disk) को manage करता है
- सभी processes को control करता है
- Security और access control को enforce करता है

### Q2: User Space और Kernel Space में क्या अंतर है?
**Answer:**
```
User Space:
- जहां आम applications चलती हैं
- Limited privileges
- Kernel की services को System Calls से लेती हैं
- यहां एक process crash हो तो system ठीक रहता है

Kernel Space:
- Kernel यहां चलता है
- Full hardware access
- महत्वपूर्ण resources को manage करता है
- यहां crash हो तो पूरा system crash हो जाता है
```

### Q3: System Calls क्या हैं?
**Answer:**
System Calls वह interface हैं जिनसे user programs kernel की services use करते हैं।

Examples:
- open() - file को open करना
- read() - file से read करना
- write() - file में write करना
- fork() - नई process बनाना

---

## 📝 Assignment

### Assignment: Architecture Diagram बनाएं

अपने हाथों से Linux architecture का diagram बनाएं जिसमें:
1. Hardware layer
2. Kernel layer
3. Device drivers
4. User space
5. Applications

---

# 3️⃣ Linux Distributions (Linux वितरण)

## 🎓 Theory

### Linux Distribution क्या है?

Linux की एक **pre-packaged version** जिसमें:
```
Linux Kernel + GNU Utilities + Package Manager + Extra Software
```

### मुख्य Linux Distributions

#### 1. **Ubuntu** (सबसे शुरुआती के लिए सही)
```
✅ Pros:
- सबसे user-friendly
- बहुत documentation available
- बड़ा community
- LTS version (3-5 years support)

❌ Cons:
- Canonical के control में
- कुछ corporate features paid हैं

💼 Use Cases:
- Learning के लिए best
- Desktop systems
- Server systems (LTS versions)
- Cloud instances

📦 Package Manager: apt, snap
```

#### 2. **CentOS** (Production Servers के लिए)
```
✅ Pros:
- RHEL का free version
- बहुत stable
- 10 years support
- Enterprise-focused

❌ Cons:
- Bleeding edge features नहीं आती
- कम documentation

💼 Use Cases:
- Production servers
- Enterprise systems
- Web hosting

📦 Package Manager: yum, dnf
```

#### 3. **RHEL (Red Hat Enterprise Linux)** (Enterprise के लिए)
```
✅ Pros:
- Enterprise support
- बहुत security focus
- Certified components
- Long-term stability

❌ Cons:
- Paid subscription
- महंगा

💼 Use Cases:
- Large enterprises
- Mission-critical systems

📦 Package Manager: yum, dnf
```

#### 4. **Debian** (Developers के लिए)
```
✅ Pros:
- बहुत stable
- सबसे ज्यादा packages available
- Desktop-friendly
- Community-driven

❌ Cons:
- Slow release cycle
- कुछ बार outdated packages

💼 Use Cases:
- Desktop systems
- Development environments

📦 Package Manager: apt
```

### Comparison Table

| Feature | Ubuntu | CentOS | RHEL | Debian |
|---------|--------|--------|------|--------|
| Release Cycle | 6 months | ~1 year | ~1 year | ~2 years |
| LTS Support | 5 years | 10 years | 10 years | 5 years |
| Beginner Friendly | ✅ Best | ❌ Hard | ❌ Hard | ✅ Good |
| Enterprise Use | ⚠️ Medium | ✅ High | ✅ Highest | ⚠️ Medium |
| Cost | Free | Free | $ $ $ | Free |

---

## 💡 Real-world Examples

### Example 1: एक Web Hosting Company

```
उनके 1000 Servers:
├── 700 CentOS servers (web hosting के लिए stable)
├── 200 Ubuntu servers (newer features के लिए)
└── 100 Debian servers (custom applications के लिए)

क्यों?
- CentOS: बहुत stable, कम updates, production के लिए safe
- Ubuntu: नए features, flexible, growing applications
- Debian: extra control, custom configurations के लिए
```

### Example 2: आपका Learning Journey

```
आप अभी शुरू कर रहे हो तो:
👍 Ubuntu 22.04 LTS का use करें

क्यों?
- सबसे ज्यादा tutorials Ubuntu पर मिलेंगे
- बड़ा community
- Beginner-friendly
- 5 years support
- VirtualBox में आसानी से install होता है
```

---

## 🧪 Hands-on Lab 1.3: Distribution Check करना

```bash
# Check करें आप कौन सा distribution use कर रहे हो

# Method 1:
cat /etc/os-release

# Output Example:
# NAME="Ubuntu"
# VERSION="22.04.1 LTS"
# ID=ubuntu
# VERSION_ID=22.04

# Method 2:
lsb_release -a

# Method 3:
cat /etc/issue

# Check करें:
# 1. Distribution का नाम
# 2. Version number
# 3. Support duration
```

---

## ❓ Interview Questions

### Q1: कितने popular Linux distributions हैं?
**Answer:**
मुख्य distributions:
1. Ubuntu - desktop और server दोनों के लिए
2. CentOS - enterprise servers के लिए
3. RHEL - corporate के लिए
4. Debian - developers के लिए
5. Fedora - latest features के लिए
6. Alpine - minimal और container के लिए

### Q2: Ubuntu और CentOS में क्या अंतर है?
**Answer:**
```
Ubuntu:
- Debian-based
- apt package manager
- 6 months release cycle
- LTS 5 years support
- Community-driven
- Desktop-friendly

CentOS:
- RHEL-based
- yum/dnf package manager
- ~1 year release cycle
- LTS 10 years support
- Enterprise-focused
- Production servers के लिए
```

### Q3: कौन सा distribution production में use होता है?
**Answer:**
- RHEL - enterprises
- CentOS - hosting providers
- Ubuntu LTS - modern startups
- Debian - custom applications

---

## 📝 Assignment

### Assignment: 3 Distributions को Research करें

1. **Ubuntu Research**
   - Latest version
   - Support duration
   - Package manager
   - When to use

2. **CentOS Research**
   - Latest version
   - Support duration
   - Advantages
   - Use cases

3. **Debian Research**
   - Latest version
   - Community size
   - Popularity
   - When to use

---

# 4️⃣ Installing Linux (Linux को Install करना)

## यह section बहुत important है क्योंकि practical work के लिए आपको Linux की जरूरत होगी!

---

## 🎓 Theory

### Installation के तरीके

```
1. Dual Boot (Windows के साथ)
   - फायदे: Real hardware पर काम करना
   - नुकसान: Risky, disk repartition की जरूरत

2. Virtual Machine (Recommended for Beginners) ✅
   - फायदे: Safe, आसान, experiments के लिए perfect
   - नुकसान: कम performance

3. Cloud (AWS, Azure, GCP)
   - फायदे: Real production environment
   - नुकसान: Internet की जरूरत, थोड़ा खर्च

4. Live USB
   - फायदे: Installation के बिना सीख सकते हो
   - नुकसान: Permanent installation नहीं
```

### Virtual Machine क्या है?

```
भौतिक Computer (आपका laptop):
├── Windows OS
├── 8 GB RAM
├── 500 GB Hard Disk
└── Intel Processor

Virtual Machine (VM):
├── Linux OS (Virtual)
├── 2 GB RAM (Virtual - आपके 8GB में से)
├── 20 GB Hard Disk Space (Virtual)
└── Processor access (Virtual)

Physical Computer के अंदर एक नया complete computer बनाना!
```

---

## 🧪 Hands-on Lab 1.4: VirtualBox में Ubuntu Install करना

### Prerequisites

```
✅ Your Computer में:
- कम से कम 8 GB RAM
- 50 GB free disk space
- Virtualization enabled (BIOS में)

📥 Download करें:
1. VirtualBox: https://www.virtualbox.org/
2. Ubuntu 22.04 LTS ISO: https://ubuntu.com/download/desktop
```

### Step-by-Step Installation Guide

#### Step 1: VirtualBox Download और Install करें

```bash
Windows पर:
1. VirtualBox website खोलें
2. Windows version download करें
3. .exe file को double-click करें
4. Next > Next > Install > Finish
5. Restart करें
```

#### Step 2: Virtual Machine बनाएं

```
1. VirtualBox खोलें
2. "New" button दबाएं
3. Dialog box fill करें:
   - Name: Linux-Learning
   - Machine Folder: Default रखें
   - Type: Linux
   - Version: Ubuntu (64-bit)
   - Memory: 2048 MB (2 GB)
   - Hard disk: Create a virtual hard disk now
   
4. VDI format चुनें
5. Dynamically allocated चुनें
6. 20 GB size दें
7. Create करें
```

#### Step 3: VM को Ubuntu ISO के साथ Configure करें

```
1. बनाए गए VM को select करें
2. "Settings" खोलें
3. Storage > Controller IDE में click करें
4. "Empty" को select करें
5. "Choose a disk file" icon दबाएं
6. Ubuntu ISO file select करें
7. OK करें
```

#### Step 4: Ubuntu Install करें

```
1. VM को double-click करें (या "Start" दबाएं)
2. Ubuntu boot होगा
3. "Install Ubuntu" option चुनें
4. Keyboard layout: English
5. Installation type: Erase disk and install Ubuntu
6. Time zone: Check करें
7. User account बनाएं:
   - Your name: अपना नाम (e.g., John)
   - Your computer's name: linux-admin (hostname)
   - Username: john
   - Password: कुछ secure password चुनें
8. Installation complete होने तक wait करें (~10-15 minutes)
9. Restart करें
```

#### Step 5: Installation Verify करें

```bash
# VM restart होने के बाद, ये commands run करें:

# Ubuntu version check करें
cat /etc/os-release

# Kernel version
uname -a

# System uptime
uptime

# Processor info
nproc

# RAM info
free -h

# Disk info
df -h /
```

---

## ✅ Verification Checklist

```
Installation Complete होने से पहले check करें:

☑️ Ubuntu successfully boot हो रहा है
☑️ GUI (desktop) display हो रहा है
☑️ आप terminal खोल सकते हो
☑️ Internet connection काम कर रहा है
☑️ apt update & apt upgrade बिना error चले
☑️ Shared folder (optional) configure हो गई है
```

---

## 🎓 Understanding Boot Process

### VM को Start करने पर क्या होता है?

```
1. BIOS (Basic Input Output System) start होती है
   - Hardware को initialize करता है
   - Bootable device को find करता है

2. Bootloader (GRUB) load होता है
   - Hard disk के first sector से
   - Linux kernel को load करता है

3. Linux Kernel Load होता है
   - Kernel को memory में load करता है
   - Hardware को initialize करता है
   - Init process start करता है

4. Init Process (systemd) start होती है
   - सभी services को start करता है
   - User login screen दिखाता है

5. Login Screen display होती है
   - User को username/password मांगता है
   - User login करता है

6. Desktop Environment (Ubuntu के लिए GNOME) load होता है
   - Desktop icons दिखाई देते हैं
   - Applications run के लिए ready हो जाते हैं
```

---

## 📝 Assignments

### Assignment 1: System Documentation

```bash
अपने नए Ubuntu VM में ये information collect करें:

1. OS Details:
   - Distribution: ___________
   - Version: ___________
   - Kernel Version: ___________

2. Hardware Details:
   - Processor: ___________
   - RAM: ___________
   - Hard Disk: ___________

3. Network:
   - Hostname: ___________
   - IP Address: ___________

4. User:
   - Username: ___________
   - Home Directory: ___________
```

### Assignment 2: First Commands

```bash
Terminal में ये commands run करें और output को note करें:

1. whoami
2. pwd
3. id
4. uname -a
5. lsb_release -a
6. cat /proc/cpuinfo
7. free -h
8. df -h
```

---

# 5️⃣ Linux Boot Process (Linux बूट प्रक्रिया)

## 🎓 Theory

### Complete Boot Sequence

```
┌─────────────────────────────────────────────────────┐
│ PHASE 1: BIOS (Basic Input/Output System)           │
│ • Computer को turn on करते ही start होता है        │
│ • Hardware को check करता है (POST - Power On Self Test)
│ • Bootable device को find करता है                   │
│ • Bootloader को load करता है                        │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ PHASE 2: Bootloader (GRUB - Grand Unified Bootloader)
│ • Hard disk के first sector से load होता है         │
│ • Linux Kernel को memory में load करता है          │
│ • Boot parameters को pass करता है kernel को        │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ PHASE 3: Kernel Loading (Linux Kernel)              │
│ • /boot/vmlinuz-* file को load करता है             │
│ • Memory को initialize करता है                     │
│ • Device drivers को load करता है                   │
│ • File system को mount करता है                     │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ PHASE 4: Init Process (systemd)                     │
│ • PID 1 की process बनती है                         │
│ • /etc/systemd/system/default.target load करता है │
│ • सभी services को start करता है                   │
│ • /etc/fstab के according filesystems mount करता है
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ PHASE 5: RunLevel/Target (Multi-user/Graphical)     │
│ • Multi-user mode: सिर्फ text interface             │
│ • Graphical mode: Desktop environment               │
│ • Network services start होती हैं                  │
│ • User login के लिए system ready हो जाता है       │
└─────────────────────────────────────────────────────┘
```

### हर Phase में क्या Files Involved हैं

```
Phase 1: BIOS
├── Hardware firmware (ROM में stored)
└── Hard disk का first sector (MBR - Master Boot Record)

Phase 2: Bootloader
├── /boot/grub/grub.cfg (GRUB configuration)
└── /boot/vmlinuz-* (Kernel file)

Phase 3: Kernel
├── /boot/initramfs-*.img (Initial RAM filesystem)
└── /boot/System.map (Symbol table)

Phase 4-5: Init
├── /etc/systemd/system/default.target
├── /etc/systemd/system/ (सभी services)
├── /etc/fstab (filesystems)
└── /etc/hostname (hostname setting)
```

---

## 💡 Real-world Example: Boot Process को Monitor करना

```bash
# Boot के detailed logs देखें:
journalctl -b -0

# या देखें kernel के messages:
dmesg | head -30

# System के current target/runlevel देखें:
systemctl get-default

# सभी loaded services देखें:
systemctl list-units --type=service --state=running
```

---

## 🧪 Hands-on Lab 1.5: Boot Process को Understand करना

```bash
# Step 1: GRUB configuration देखें
sudo nano /boot/grub/grub.cfg
# (read-only, "q" से exit करें)

# Step 2: Kernel files देखें
ls -la /boot/

# Output:
# -rw-r--r-- 1 root root  13982 Nov 22 11:14 config-5.15.0-56-generic
# -rw-r--r-- 1 root root  76484 Nov 22 11:14 System.map-5.15.0-56-generic
# -rw-r--r-- 1 root root 149710 Nov 22 11:14 initrd.img-5.15.0-56-generic
# -rw-x--x-- 1 root root   14288 Nov 22 11:14 vmlinuz-5.15.0-56-generic

# Step 3: Boot sequence देखें
sudo journalctl -b | head -50

# Step 4: Current runlevel/target देखें
systemctl get-default
# Output: graphical.target या multi-user.target

# Step 5: Services जो boot पर start होते हैं:
systemctl list-unit-files --type=service | grep enabled

# Step 6: Boot time कितना था?
systemd-analyze

# Output:
# Startup finished in 3.456s (kernel) + 5.234s (userspace) = 8.690s
```

---

## ❓ Interview Questions

### Q1: Linux Boot Process के phases कौन-कौन से हैं?
**Answer:**
1. BIOS - Hardware initialization
2. Bootloader (GRUB) - Kernel को load करना
3. Kernel Loading - Kernel initialization
4. Init Process (systemd) - System initialization
5. RunLevel/Target - Multi-user या graphical mode

### Q2: GRUB क्या है?
**Answer:**
GRUB (Grand Unified Bootloader) एक bootloader है जो:
- Hard disk से Linux kernel को load करता है
- Multiple operating systems को boot करने की capability देता है
- Boot parameters को customize करने की सुविधा देता है
- BIOS और kernel के बीच interface प्रदान करता है

---

# 6️⃣ Linux Directory Structure (Linux निर्देशिका संरचना)

## 🎓 Theory

### Linux का Root Directory Structure

```
/ (Root)
├── /bin          → Essential command binaries (ls, cat, chmod, etc)
├── /boot         → Boot related files (kernel, initramfs, grub)
├── /dev          → Device files (drives, terminals, printers)
├── /etc          → System configuration files
├── /home         → User home directories
├── /lib          → System libraries
├── /lib64        → 64-bit system libraries
├── /media        → Mount points for removable media
├── /mnt          → Temporary mount points
├── /opt          → Optional software packages
├── /proc         → Process information (virtual filesystem)
├── /root         → Root user's home directory
├── /run          → Runtime data
├── /sbin         → System binaries (only root can use)
├── /srv          → Service data
├── /sys          → System information (virtual filesystem)
├── /tmp          → Temporary files
├── /usr          → User applications and libraries
├── /var          → Variable data (logs, caches, mail)
└── /lost+found   → Recovered files after crash
```

### महत्वपूर्ण Directories विस्तार से

#### `/bin` - Essential Commands
```bash
# Location: /bin
# Purpose: Essential command binaries जो सभी को चाहिए

Examples:
/bin/ls       → list files command
/bin/cat      → concatenate files command
/bin/chmod    → change permissions command
/bin/cp       → copy command
/bin/mv       → move command
/bin/rm       → remove command
/bin/mkdir    → make directory command
/bin/bash     → bash shell

# यह commands single-user mode में भी available होते हैं
```

#### `/etc` - Configuration Files
```bash
# Location: /etc
# Purpose: सभी system configuration files

Important files:
/etc/hostname          → System का नाम
/etc/fstab             → Filesystems की information
/etc/passwd            → User accounts की information
/etc/shadow            → Encrypted passwords
/etc/group             → Group information
/etc/sudoers           → Sudo permissions
/etc/systemd/          → systemd configuration
/etc/network/          → Network configuration
/etc/ssh/sshd_config   → SSH server configuration
```

#### `/home` - User Directories
```bash
# Location: /home
# Purpose: हर user के अपने directory

Example:
/home/john/           → John user का directory
/home/john/Desktop/   → Desktop files
/home/john/Documents/ → Documents
/home/john/Downloads/ → Downloaded files
/home/john/Pictures/  → Pictures
/home/john/Videos/    → Videos
/home/john/.bashrc    → Bash configuration file
/home/john/.ssh/      → SSH keys directory
```

#### `/tmp` - Temporary Files
```bash
# Location: /tmp
# Purpose: Temporary files store करना

Features:
- World-writable directory
- कोई भी user यहां write कर सकता है
- Reboot के बाद clear हो जाता है
- पुरानी files automatically delete हो जाती हैं

Use:
- Temporary data store करना
- Large files को temporarily download करना
```

#### `/var` - Variable Data
```bash
# Location: /var
# Purpose: Changing data जो over time बढ़ता है

Important subdirectories:
/var/log/              → System logs
  /var/log/syslog      → System messages
  /var/log/auth.log    → Authentication logs
  /var/log/kernel.log  → Kernel logs
  
/var/cache/            → Application cache

/var/mail/             → User mailboxes

/var/lib/              → Application data

/var/run/              → Runtime data (PID files)
```

#### `/root` - Root User's Home
```bash
# Location: /root
# Purpose: root user (superuser) का home directory

Note:
- Only root can access this
- Regular users का /home में directory है
- root का /root में है
```

#### `/proc` - Virtual Filesystem
```bash
# Location: /proc
# Purpose: Process और system information provide करना

Examples:
/proc/cpuinfo          → CPU information
/proc/meminfo          → Memory information
/proc/version          → Kernel version
/proc/[PID]/           → Specific process information
/proc/[PID]/cmdline    → Process का command line
/proc/[PID]/maps       → Process की memory mapping

यह filesystem virtual है - disk पर actually files नहीं हैं!
```

---

## 💡 Real-world Example

### Example: एक File की Journey

```
मान लो आप एक file create करते हो:
$ nano /home/john/myfile.txt

क्या होता है:
1. /home directory में जाता है
   /home/
   
2. john user का directory खोलता है
   /home/john/
   
3. यहां myfile.txt create करता है
   /home/john/myfile.txt
   
4. nano editor सब से पहले:
   /etc/nanorc configuration file पढ़ता है
   /var/tmp/ में temporary file बनाता है
   
5. File save होती है:
   /home/john/myfile.txt में
   
6. File की metadata:
   /etc/fstab से filesystem की info लेता है
   /proc से system info लेता है
```

---

## 🧪 Hands-on Lab 1.6: Directory Structure को Explore करना

```bash
# Step 1: Root directory की सभी files/folders देखें
ls -la /

# Step 2: /bin में commands देखें
ls /bin | head -20

# Step 3: /etc में configuration files
ls /etc | head -20

# Step 4: /var में data देखें
ls /var

# Step 5: /home में user directories
ls /home

# Step 6: /tmp को explore करें
ls -la /tmp

# Step 7: /proc से CPU info
cat /proc/cpuinfo | head -15

# Step 8: /proc से memory info
cat /proc/meminfo | head -10

# Step 9: अपने current directory को know करो
pwd

# Step 10: Home directory में जाओ
cd ~
pwd

# Step 11: सभी files को (hidden भी) देखो
ls -la
```

---

## ❓ Interview Questions

### Q1: Linux में root directory `/` क्या है?
**Answer:**
Root directory (`/`) Linux filesystem का सबसे ऊपरी directory है। सभी other directories और files इसी के अंदर हैं।

### Q2: `/bin` और `/sbin` में क्या अंतर है?
**Answer:**
```
/bin:
- Essential commands
- सभी users use कर सकते हैं
- Single-user mode में भी available
- Examples: ls, cat, cp, mv

/sbin:
- System binaries
- सिर्फ root user use कर सकते हैं
- Administrative tasks के लिए
- Examples: fdisk, parted, ifconfig
```

### Q3: `/etc/passwd` क्या file है?
**Answer:**
यह एक text file है जिसमें सभी user accounts की information है। इसमें:
- Username
- User ID (UID)
- Group ID (GID)
- Home directory
- Shell
- (Password `/etc/shadow` में है)

### Q4: `/proc` virtual filesystem क्यों है?
**Answer:**
`/proc` एक virtual filesystem है जो kernel द्वारा on-the-fly create किया जाता है। यह:
- Real disk पर files नहीं हैं
- System के running information को provide करता है
- Processes, CPU, memory, network information देता है
- Read-only होती है अधिकतर

---

## 📝 Assignments

### Assignment 1: Directory Tree बनाएं

```bash
अपने Linux system का directory structure draw करें:

Level 1: / (root)
├── /bin
├── /etc
├── /home
├── /tmp
├── /var
└── ... (others)

Level 2 (for /etc):
/etc
├── /etc/passwd
├── /etc/shadow
├── /etc/group
└── ... (others)
```

### Assignment 2: Important Files को Document करें

```
Important configuration files:
1. /etc/hostname - Purpose:_________ Path:_________
2. /etc/fstab - Purpose:_________ Path:_________
3. /etc/passwd - Purpose:_________ Path:_________
4. /etc/sudoers - Purpose:_________ Path:_________
5. /etc/ssh/sshd_config - Purpose:_________ Path:_________
```

### Assignment 3: Directory Navigation

```bash
Terminal में run करें:

1. pwd - Show current directory
2. cd / - Go to root
3. cd /etc - Go to /etc
4. ls - List files
5. cd /home - Go to /home
6. cd ~ - Go to home directory
7. pwd - Show current directory
```

---

## 🎯 Phase 1 Summary (सारांश)

### आपने सीखा:
- ✅ Linux क्या है और इसका इतिहास
- ✅ Linux का architecture कैसे काम करता है
- ✅ مختلف Linux distributions में अंतर
- ✅ VirtualBox में Ubuntu कैसे install करें
- ✅ Linux boot process कैसे काम करती है
- ✅ Linux directory structure कैसी organized है

### अगला Phase:
**Phase 2: Linux Commands** - 20 days में सभी important commands सीखेंगे

---

**Status: Phase 1 Complete ✅**  
**Next: Phase 2 - Linux Commands Foundation**  
**Time Investment: ~5-6 hours per day**  
**Total Days: 5 days**

