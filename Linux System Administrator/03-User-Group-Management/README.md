# PHASE 3: User & Group Management

## 📚 Phase Overview

**Duration:** 8 Days  
**Time Commitment:** 4-5 hours/day  
**Prerequisites:** Phase 1 & 2 complete  
**Difficulty:** Intermediate  
**Importance:** ⭐⭐⭐⭐⭐ (Very Critical for Linux Admin)

---

## 🎯 What You'll Learn

By the end of this phase, you will be able to:

✅ Create, modify, and delete Linux users
✅ Manage groups efficiently
✅ Configure user permissions
✅ Properly setup sudo access
✅ Implement password policies
✅ Ensure user security
✅ Handle real-world user scenarios  

---

## 📖 Topics Breakdown

### Day 1: User Basics & Understanding /etc/passwd

**Topics:**
- User concept
- UID (User ID) क्या है
- GID (Group ID) क्या है
- /etc/passwd file structure
- /etc/shadow file understanding
- User types (system, regular, root)

**Key Learnings:**
```
/etc/passwd format:
username:password:UID:GID:GECOS:home_dir:login_shell

Example:
john:x:1000:1000:John User:/home/john:/bin/bash
│    │  │    │    │          │            └─ Login shell
│    │  │    │    │          └─ Home directory
│    │  │    │    └─ Full name
│    │  │    └─ Primary GID
│    │  └─ UID
│    └─ Password (encrypted in /etc/shadow)
└─ Username

Important UIDs:
0     = root (superuser)
1-999 = System users
1000+ = Regular users
```

**Lab 3.1:**
```bash
# /etc/passwd को examine करना
cat /etc/passwd
head -5 /etc/passwd

# /etc/shadow को देखना (sudo की जरूरत)
sudo cat /etc/shadow | head -5

# Specific user की info
grep john /etc/passwd

# User की UID check करना
id john
```

**Interview Questions:**
1. UID 0 और 1000 में क्या अंतर है?
2. /etc/passwd में passwords नहीं होते - क्यों?
3. Shadow file का क्या purpose है?

---

### Day 2-3: User Creation & Management

**Day 2: Creating Users**

**Topics:**
- `useradd` command
- `adduser` command (interactive)
- Default values
- Home directory creation
- Shell selection

**Key Commands:**

```bash
# Simple user create करना
sudo useradd john

# Home directory के साथ
sudo useradd -m -d /home/john john

# Specific shell के साथ
sudo useradd -m -s /bin/bash john

# Interactive way (Ubuntu)
sudo adduser john

# Check करना
id john
cat /etc/passwd | grep john
```

**Lab 3.2:**
```bash
# 5 users create करो
sudo useradd -m user1
sudo useradd -m user2
sudo useradd -m user3
sudo useradd -m user4
sudo useradd -m user5

# सभी users check करो
grep "user[1-5]" /etc/passwd
```

**Day 3: Modifying & Deleting Users**

**Topics:**
- `usermod` command
- Changing username, UID
- Adding/removing groups
- Shell को change करना
- Account expiration

**Key Commands:**

```bash
# UID change करना
sudo usermod -u 2000 john

# Groups में add करना
sudo usermod -aG sudo john

# Shell change करना
sudo usermod -s /bin/bash john

# Account expiration set करना
sudo usermod -e 2025-12-31 john

# User को lock करना
sudo usermod -L john

# User को unlock करना
sudo usermod -U john
```

**Interview Questions:**
1. usermod -a vs usermod (difference क्या है)?
2. User को delete करते समय files को क्या करते हो?
3. Account expiration कब use होता है?

---

### Day 4: Group Management

**Topics:**
- `groupadd`, `groupmod`, `groupdel`
- /etc/group structure
- Primary vs Secondary groups
- Group membership management

**Key Commands:**

```bash
# Group create करना
sudo groupadd developers

# Group को modify करना (name change)
sudo groupmod -n newdevs developers

# User को group में add करना
sudo usermod -aG developers john

# Group को delete करना
sudo groupdel developers

# Groups check करना
cat /etc/group
groups john
```

**Lab 3.3:**
```bash
# 3 groups create करो
sudo groupadd developers
sudo groupadd admins
sudo groupadd testers

# Users को groups में add करो
sudo usermod -aG developers user1
sudo usermod -aG admins user2
sudo usermod -aG testers user3

# Verify करो
grep "developers\|admins\|testers" /etc/group
```

---

### Day 5: Password Management

**Topics:**
- `passwd` command
- Password aging
- `chage` command
- /etc/login.defs
- Strong password policies

**Key Commands:**

```bash
# User का password set करना
sudo passwd john

# Password को expire करना
sudo passwd -e john

# Password history देखना
sudo chage -l john

# Password policy set करना
sudo chage -M 90 john    # Max 90 days
sudo chage -m 1 john     # Min 1 day
sudo chage -W 7 john     # Warning 7 days before

# Account expire करना
sudo chage -E 2025-12-31 john

# Root password change करना
sudo passwd
```

**Interview Questions:**
1. Strong password policy क्या होती है?
2. Password aging क्यों important है?

---

### Day 6: Sudo Access & Privileges

**Topics:**
- Sudo क्या है
- Sudoers file
- Sudo rules syntax
- Specific command sudo access
- Sudo without password

**Key Commands:**

```bash
# Sudo user को बनाना
sudo usermod -aG sudo john

# Sudoers file को edit करना (SAFE WAY)
sudo visudo

# Example entries:
# john ALL=(ALL) ALL              # सभी commands
# %developers ALL=(ALL) ALL       # पूरे group को
# john ALL=(ALL) NOPASSWD: /bin/ls  # Password के बिना specific command

# Check current sudo access
sudo -l

# Specific command को run करना
sudo systemctl restart nginx
```

**Lab 3.4: Sudo Access Configuration**

```bash
# User को sudo access दो
sudo usermod -aG sudo john

# Specific command access दो (visudo से)
sudo visudo

# Add this line:
# john ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart nginx

# Test करो
sudo systemctl restart nginx  # Password नहीं मांगेगा
```

**Interview Questions:**
1. Sudoers file को directly edit क्यों नहीं करते?
2. NOPASSWD क्यों security risk हो सकता है?

---

### Day 7-8: Hands-on Labs & Project

**Lab 3.5: Complete User Management Scenario**

```bash
# Scenario: एक web hosting company के लिए user setup करना

# Step 1: Groups create करो
sudo groupadd webadmins
sudo groupadd webusers
sudo groupadd dbadmins

# Step 2: 3 admin users create करो
sudo useradd -m -s /bin/bash -G webadmins admin1
sudo useradd -m -s /bin/bash -G webadmins admin2
sudo useradd -m -s /bin/bash -G dbadmins dba1

# Step 3: 5 regular users create करो
for i in {1..5}; do
  sudo useradd -m -s /bin/bash user$i
  sudo usermod -aG webusers user$i
done

# Step 4: Password set करो
for i in {1..5}; do
  echo "user$i:password$i" | sudo chpasswd
done

# Step 5: Sudo access configure करो
sudo visudo
# Add:
# %webadmins ALL=(ALL) ALL
# %dbadmins ALL=(ALL) NOPASSWD: /usr/bin/systemctl

# Step 6: Verify करो
cat /etc/passwd | grep user
grep "webadmins\|webusers\|dbadmins" /etc/group
id user1
```

**Lab 3.6: Password Policy Implementation**

```bash
# Strong password policy set करो
for user in user1 user2 user3; do
  sudo chage -M 60 $user    # Password validity 60 days
  sudo chage -m 1 $user     # Min 1 day before change
  sudo chage -W 7 $user     # Warning 7 days
  sudo chage -I 30 $user    # Inactive for 30 days = lock
done

# Policy verify करो
sudo chage -l user1
```

---

## 🎯 Real-world Scenarios

### Scenario 1: नया Developer को Onboard करना

```bash
# नया developer John को system में add करना

# Step 1: User create करो
sudo useradd -m -s /bin/bash john

# Step 2: Developer group में add करो
sudo usermod -aG developers john

# Step 3: Temporary password दो
sudo passwd john
# User को कहो कि first login पर password change करे

# Step 4: SSH key setup करो
sudo mkdir -p /home/john/.ssh
sudo chmod 700 /home/john/.ssh
sudo chown john:john /home/john/.ssh

# Step 5: Sudo permissions दो
sudo visudo
# Add: john ALL=(ALL) NOPASSWD: /usr/bin/systemctl

# Verify करो
id john
groups john
```

### Scenario 2: Contractor को Limited Access देना

```bash
# Contractor को specific commands के लिए access

sudo visudo
# Add:
# contractor ALL=(ALL) NOPASSWD: /usr/bin/systemctl status
# contractor ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart nginx
# contractor ALL=(ALL) NOPASSWD: /bin/ls /var/www

# यह सिर्फ ये 3 commands run कर सकेगा
```

---

## 📝 Practice Assignments

### Assignment 1: User Management Operations

```bash
सभी operations को manually करो:

1. 10 users create करो (user1 से user10)
2. 3 groups create करो (admin, developer, user)
3. Users को groups में add करो
4. सभी users का password set करो
5. एक user को lock करो
6. एक user का shell change करो
7. एक user को sudo दो
8. सभी changes verify करो
```

### Assignment 2: Security Audit

```bash
अपने system का security audit करो:

[ ] सभी users को list करो
[ ] System users vs Regular users identify करो
[ ] Weak UIDs को find करो
[ ] Sudo users को list करो
[ ] Password policies को check करो
[ ] Dormant accounts को identify करो
[ ] Security recommendations दो
```

---

## ✅ Success Criteria

इस phase को complete मानने से पहले, आप यह सब कर सकते हो:

✅ 10+ users को create और manage करो  
✅ Multiple groups को efficiently manage करो  
✅ Sudo access को properly configure करो  
✅ Password policies को implement करो  
✅ Real-world scenarios को handle करो  
✅ User security को ensure करो  
✅ Interview questions को सही से जवाब दो  

---

## 🔗 Related Phases

**After This Phase:**
- PHASE 4: File Permissions (Users के permissions को control करने के लिए)
- PHASE 10: Security (User security को further strengthen करने के लिए)

**Before This Phase:**
- PHASE 1: Linux Fundamentals ✅
- PHASE 2: Linux Commands ✅

---

**Next Step: Go to Day 1 - User Basics & /etc/passwd**

**Time to Master User Management! 🚀**

