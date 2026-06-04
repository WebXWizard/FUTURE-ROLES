# Phase 04: File & Directory Permissions (10 Days)

> Learn how to lock files and directories in Linux. This is the foundation of security. Understand who can read, who can write, and who can execute using chmod, chown, and chgrp commands.

**Phase Duration**: 10 days  
**Prerequisites**: Complete Phase 1, 2, 3  
**Time Commitment**: 4-5 hours per day

---

## 📋 Phase 04 Introduction

### Why This Is Important

```
If Linux is a house:
├── chmod = changing locks (who can enter)
├── chown = changing owner (whose house is it)
├── chgrp = giving permission to group members
├── ACL = specific people get specific rights
└── SUID/SGID = temporary admin rights (for specific commands)

Without understanding this:
❌ Wrong people can get access
❌ Security breaches can happen
❌ System settings can get corrupted
```

### What You'll Learn

- ✅ What are file permissions (r, w, x)
- ✅ Octal notation (755, 644, 777)
- ✅ Symbolic notation (u+rwx, g-w, o+r)
- ✅ chmod command in all methods
- ✅ Changing ownership with chown/chgrp
- ✅ Special permissions (SUID, SGID, Sticky Bit)
- ✅ ACLs (Advanced Access Control Lists)
- ✅ Real-world security scenarios
- ✅ Common mistakes and troubleshooting

---

## 🗓️ Day-by-Day Detailed Guide

### **DAY 1: File Permissions Fundamentals**

#### 📖 Theory

**What is a Permission?**

Every file/directory in Linux has 3 types of permissions:

```
r (Read)    = 4  = Permission to read content
w (Write)   = 2  = Permission to change/write content
x (Execute) = 1  = Permission to run program (for files)
                  = Permission to open folder (for directories)
```

**Who gets permissions?**

```
u (User/Owner)  = The person who created the file
g (Group)       = All users in the same group
o (Others)      = Everyone else (world)
a (All)         = All categories (u+g+o)
```

**Understanding Permission Strings:**

```bash
$ ls -l /etc/passwd
-rw-r--r-- 1 root root 2341 Nov 15 10:30 /etc/passwd
 ^^^^^^^^^^
 First - = regular file
 Next 9 characters:
  rw-  = owner has read+write (6)
  r--  = group has read only (4)
  r--  = others have read only (4)
 
 So this is 644 permission
```

**Visual Representation:**

```
Permission String: -rwxr-x--x
                   ^^^-^^-^^-
                   ||+-+++-+++---- others (1,2,4 = x,w,r)
                   ||  |  |-------- group (5,2,4 = x,r,w)
                   ||  |----------- user (7,2,4 = x,r,w)
                   |+-------------- file type (- = file, d = dir, l = link)

Result = -rwxr-x--x = 751
         (user=7, group=5, others=1)
```

---

#### 🧪 Lab 1.1: Understanding Permission Strings

```bash
# Step 1: एक test file बनाएं
mkdir -p ~/test-permissions
cd ~/test-permissions
touch demo.txt
ls -l demo.txt

# Default output:
# -rw-r--r-- 1 user group 0 May 30 10:00 demo.txt

# Step 2: Break down the permission string
# -      rw-    r--    r--
# Type   User   Group  Others
# file   (6)    (4)    (4)

# Practice: इन permissions को समझें
echo "rw-r--r--" >> ~/demo_notes.txt  # 644
echo "rwxr-xr-x" >> ~/demo_notes.txt  # 755
echo "rw-------" >> ~/demo_notes.txt  # 600
echo "rwxrwxrwx" >> ~/demo_notes.txt  # 777
```

---

### **DAY 2: chmod Command - Octal Notation**

#### 📖 सिद्धांत

**chmod = "change mode" (permissions बदलना)**

**Octal Method (Numeric):**

```
Number    = Permission
0         = --- (कोई permission नहीं)
1         = --x (execute only)
2         = -w- (write only)
3         = -wx (write + execute)
4         = r-- (read only)
5         = r-x (read + execute)
6         = rw- (read + write)
7         = rwx (सभी permissions)
```

**Formula**: chmod [user][group][others] filename

```bash
chmod 755 script.sh
      ^^^
      ||| 
      ||+-- others: 5 (r-x)
      |+--- group:  5 (r-x)
      +---- user:   7 (rwx)
```

---

#### 🧪 Lab 2.1: chmod का Octal तरीका

```bash
cd ~/test-permissions

# Step 1: File बनाएं और default permission देखें
touch file1.txt file2.sh file3.log
ls -l
# सभी में -rw-r--r-- (644) होगा

# Step 2: User को full access दें (700)
chmod 700 file1.txt
ls -l file1.txt
# Output: -rwx------ अब सिर्फ owner को access है

# Step 3: Owner + Group को read करने दें (640)
chmod 640 file2.sh
ls -l file2.sh
# Output: -rw-r----- owner को rw, group को r

# Step 4: सभी को read दें, कोई write न कर सके (444)
chmod 444 file3.log
ls -l file3.log
# Output: -r--r--r-- सभी को सिर्फ read

# Step 5: Write करने का प्रयास करें
echo "test" >> file3.log
# Output: -bash: file3.log: Permission denied ✓

# Step 6: Permission वापस बदलें
chmod 644 file3.log
echo "test" >> file3.log  # अब काम करेगा ✓
```

---

### **DAY 3: chmod Command - Symbolic Notation**

#### 📖 सिद्धांत

**Symbolic Method (को समझना आसान है):**

```
chmod [who][operation][permission] filename

who:
  u = user (owner)
  g = group
  o = others
  a = all (default)

operation:
  + = permission add करो
  - = permission remove करो
  = = set करो (बाकी सब remove हो जाएंगी)

permission:
  r = read (4)
  w = write (2)
  x = execute (1)
```

**Examples:**

```bash
chmod u+x file.sh      # User को execute permission दो
chmod g-w file.txt     # Group से write हटाओ
chmod o=r file.log     # Others को सिर्फ read दो (बाकी remove)
chmod a+r file.txt     # सभी को read दो
chmod u+rwx file.sh    # User को सभी permissions दो
```

---

#### 🧪 Lab 3.1: chmod का Symbolic तरीका

```bash
cd ~/test-permissions

# Step 1: Files बनाएं
touch script.sh document.txt config.conf

# Step 2: Script को executable बनाओ
chmod u+x script.sh
ls -l script.sh
# Output: -rwxr--r-- (751)

# Step 3: Document से group का write हटाओ
chmod g-w document.txt
ls -l document.txt
# Output: -rw-r--r-- (644)

# Step 4: Config को exact permissions दो
chmod u=rw,g=r,o= config.conf
ls -l config.conf
# Output: -rw-r----- (640)

# Step 5: Multiple operations एक साथ
touch multitest.txt
chmod u=rwx,g=rx,o= multitest.txt
ls -l multitest.txt
# Output: -rwxr-x--- (750)

# Step 6: Recursive apply करो (directory में)
mkdir -p project/src
chmod -R 755 project/
ls -lR project/
```

---

### **DAY 4: chown & chgrp - Ownership बदलना**

#### 📖 सिद्धांत

**chown = "change owner" (owner बदलना)**
**chgrp = "change group" (group बदलना)**

```bash
chown [new_owner] file.txt          # Owner बदलो
chown [owner]:[group] file.txt      # Owner + Group दोनों
chown :[group] file.txt             # सिर्फ Group (colon से शुरू करो)
chown -R [owner] directory/         # Recursively सभी files
```

**जरूरी: Root होना पड़ता है!**

```bash
# Regular user
$ chown newowner file.txt
chown: changing ownership of 'file.txt': Operation not permitted

# Root से करना होगा
$ sudo chown newowner file.txt  ✓
```

---

#### 🧪 Lab 4.1: chown & chgrp

```bash
cd ~/test-permissions

# Step 1: दो users बनाओ (practice के लिए)
sudo useradd developer 2>/dev/null
sudo useradd admin 2>/dev/null

# Step 2: File बनाओ (current user की होगी)
touch owned.txt
ls -l owned.txt
# Output: -rw-r--r-- yourname yourgroup 0 May 30 10:00 owned.txt

# Step 3: Owner बदलो (sudo की जरूरत है)
sudo chown developer owned.txt
ls -l owned.txt
# Output: -rw-r--r-- developer yourgroup 0 May 30 10:00 owned.txt

# Step 4: Group बदलो
sudo chgrp admin owned.txt
ls -l owned.txt
# Output: -rw-r--r-- developer admin 0 May 30 10:00 owned.txt

# Step 5: दोनों एक साथ बदलो
sudo chown root:root owned.txt
ls -l owned.txt
# Output: -rw-r--r-- root root 0 May 30 10:00 owned.txt

# Step 6: Recursive करो
mkdir -p myproject/src/components
sudo chown -R developer:admin myproject/
ls -lR myproject/
# सभी में developer:admin होगा
```

---

### **DAY 5: Special Permissions - SUID**

#### 📖 सिद्धांत

**SUID (Set User ID) क्या है?**

```
जब कोई program SUID set होता है:
├── Program चलेगा program owner के साथ
├── उसके बाद जो user चलाएगा वह नहीं (program के owner के rights से)
├── Example: passwd command
│   ├── Owner: root
│   ├── SUID: set है
│   └── जब आप चलाते हो: root के साथ चलता है
└── यह इसलिए है क्योंकि /etc/shadow को सिर्फ root change कर सकता है
```

**Visual:**

```
Normal Permission:      SUID Permission:
-rwxr-xr-x  user        -rwsr-xr-x  user
 ^^^                     ^^^
 user को rwx              SUID set है (s instead of x)
```

**SUID Set करना:**

```bash
# Method 1: Numeric (4755)
chmod 4755 script.sh
#     ^^^^ 4 = SUID

# Method 2: Symbolic
chmod u+s script.sh
# s = set user id
```

---

#### 🧪 Lab 5.1: SUID को समझना

```bash
cd ~/test-permissions

# Step 1: Real example - passwd command
ls -l /usr/bin/passwd
# Output: -rwsr-xr-x root root /usr/bin/passwd
#          ^^^ = 's' का मतलब SUID है!

# Step 2: File बनाओ जो current user print करे
cat > whoami_test.sh << 'EOF'
#!/bin/bash
echo "I am: $(whoami)"
echo "UID: $UID"
EOF

chmod +x whoami_test.sh
./whoami_test.sh
# Output: I am: yourname, UID: 1000

# Step 3: Root user switch करके SUID set करो
sudo chown root:root whoami_test.sh
sudo chmod 4755 whoami_test.sh
ls -l whoami_test.sh
# Output: -rwsr-xr-x root root whoami_test.sh

# Step 4: अब फिर से चलाओ
./whoami_test.sh
# Output: I am: root, UID: 0
# ⚠️ Notice: यह root के साथ चल रहा है!

# Step 5: SUID हटाओ
sudo chmod u-s whoami_test.sh
ls -l whoami_test.sh
# Output: -rwxr-xr-x root root whoami_test.sh
# 's' चला गया, अब 'x' है
```

---

### **DAY 6: Special Permissions - SGID & Sticky Bit**

#### 📖 सिद्धांत

**SGID (Set Group ID):**

```
chmod 2755 file.sh

Effect:
├── Program चलता है file के group के साथ
├── Directory में: सभी नई files automatically same group में जाती हैं
└── Example: /usr/local/bin में साझी scripts
```

**Sticky Bit:**

```
chmod 1777 /tmp

Effect:
├── अगर आपने file create की तो सिर्फ आप delete कर सकते हो
├── Shared directories में useful है
└── /tmp में यह default है
```

**Special Permissions Table:**

```
chmod 4755  =  SUID + rwxr-xr-x
chmod 2755  =  SGID + rwxr-xr-x
chmod 1755  =  Sticky + rwxr-xr-x
chmod 5755  =  SUID + SGID + rwxr-xr-x (rare)
chmod 7755  =  SUID + SGID + Sticky + rwxr-xr-x (very rare)
```

---

#### 🧪 Lab 6.1: SGID और Sticky Bit

```bash
cd ~/test-permissions

# Part A: SGID को समझना
# ================================

# Step 1: Shared directory बनाओ
mkdir -p shared_project
sudo chown root:developers shared_project 2>/dev/null || true
ls -ld shared_project

# Step 2: SGID set करो
sudo chmod 2770 shared_project
ls -ld shared_project
# Output: drwxrws--- root developers
#          ^^^ s = SGID है!

# Step 3: File बनाओ
touch shared_project/file1.txt
ls -l shared_project/
# Owner: आप, Group: developers (यानी SGID काम कर रहा है!)

# Part B: Sticky Bit को समझना
# ================================

# Step 4: Test directory बनाओ
mkdir -p shared_temp
chmod 1777 shared_temp
ls -ld shared_temp
# Output: drwxrwxrwt
#          ^^^^^^^ t = Sticky Bit!

# Step 5: File बनाओ
touch shared_temp/myfile.txt
ls -l shared_temp/myfile.txt

# Step 6: दूसरे user से delete करने का प्रयास करें
# (अगर multi-user system हो तो)
# यह fail होगा क्योंकि Sticky Bit है!
```

---

### **DAY 7: ACLs (Access Control Lists) - Advanced Permissions**

#### 📖 सिद्धांत

**ACL क्यों चाहिए?**

```
Standard Permissions से limitation:
chmod 755:  user को rwx, group को rx, others को rx
            लेकिन specific user को अलग permission नहीं दे सकते!

ACL से:
setfacl:    किसी specific user को specific permission दे सकते हो
            चाहे वह owner हो या group में हो या नहीं
```

**ACL Commands:**

```bash
setfacl -m u:username:rwx file.txt     # User के लिए permission set करो
setfacl -m g:groupname:rx file.txt     # Group के लिए permission set करो
getfacl file.txt                        # Current ACLs देखो
setfacl -x u:username file.txt         # User का ACL हटाओ
setfacl -R -m u:username:rx directory/ # Recursive करो
```

---

#### 🧪 Lab 7.1: ACLs का उपयोग

```bash
cd ~/test-permissions

# Step 1: Test users और file बनाओ
sudo useradd john 2>/dev/null || true
sudo useradd jane 2>/dev/null || true
touch document.txt
chmod 640 document.txt
ls -l document.txt

# Step 2: Current ACL देखो
getfacl document.txt
# Output:
# # file: document.txt
# # owner: yourname
# # group: yourgroup
# user::rw-
# group::r--
# other::---

# Step 3: jane को read-write permission दो
sudo setfacl -m u:jane:rw document.txt
getfacl document.txt
# अब jane को भी read-write दिख जाएगा!

# Step 4: john को सिर्फ read दो
sudo setfacl -m u:john:r document.txt
getfacl document.txt

# Step 5: Directory के लिए recursive ACL
mkdir project_folder
sudo setfacl -R -m u:jane:rwx project_folder
sudo setfacl -R -m u:john:rx project_folder
getfacl -R project_folder/

# Step 6: jane का access हटाओ
sudo setfacl -x u:jane document.txt
getfacl document.txt
# jane हटा दिया जाएगा!
```

---

### **DAY 8: Real-World Security Scenarios**

#### Scenario 1: Web Server Permissions

```bash
# Typical Apache/Nginx setup:

# Step 1: Web directory बनाओ
sudo mkdir -p /var/www/html/myapp
sudo chown www-data:www-data /var/www/html/myapp
sudo chmod 755 /var/www/html/myapp

# Step 2: Static files (images, CSS)
sudo chmod 644 /var/www/html/myapp/*.{html,css,js}

# Step 3: Upload directory (web server को write करना है)
mkdir /var/www/html/myapp/uploads
sudo chmod 755 /var/www/html/myapp/uploads

# Step 4: Config files (सिर्फ owner को read)
sudo chmod 600 /var/www/html/myapp/config.php

# Step 5: Security: others को कोई access न हो
sudo chmod -R o-rwx /var/www/html/myapp/
```

#### Scenario 2: Multi-User Development

```bash
# Step 1: Development group बनाओ
sudo groupadd developers
sudo usermod -aG developers john
sudo usermod -aG developers jane

# Step 2: Shared project directory
sudo mkdir -p /home/projects/app
sudo chown root:developers /home/projects/app
sudo chmod 2770 /home/projects/app  # SGID for auto-grouping

# Step 3: नई files automatically developers group में जाएंगी
cd /home/projects/app
touch README.md
ls -l README.md
# Group: developers (automatic!)

# Step 4: Private files
echo "secret" > private.txt
chmod 600 private.txt
# सिर्फ creator को access

# Step 5: Public documentation
echo "API Docs" > PUBLIC_API.md
chmod 644 PUBLIC_API.md
# सभी को read
```

#### Scenario 3: Cron Job Security

```bash
# Step 1: Backup script बनाओ
cat > backup.sh << 'EOF'
#!/bin/bash
tar czf /backups/backup-$(date +%Y%m%d).tar.gz /important/data/
EOF

# Step 2: Root के रूप में चलना है तो SUID लगाओ
sudo chown root:root backup.sh
sudo chmod 4755 backup.sh

# OR बेहतर तरीका: sudo से cron में run करो
# /etc/cron.daily/backup.sh में:
# #!/bin/bash
# /usr/local/bin/backup.sh

# Step 3: Cron file को secure रखो
sudo chmod 600 /etc/cron.d/backup-cron
```

---

#### 🧪 Lab 8.1: Web Server Permissions Setup

```bash
# Realistic scenario:

# Step 1: Structure बनाओ
mkdir -p ~/webproject/public
mkdir -p ~/webproject/private
mkdir -p ~/webproject/uploads
mkdir -p ~/webproject/config

# Step 2: Files बनाओ
echo "<h1>Public Site</h1>" > ~/webproject/public/index.html
echo "Database Password" > ~/webproject/private/db.conf
touch ~/webproject/uploads/placeholder.txt
echo "API_KEY=secret123" > ~/webproject/config/settings.php

# Step 3: Permissions set करो
chmod 755 ~/webproject/public
chmod 700 ~/webproject/private
chmod 755 ~/webproject/uploads
chmod 700 ~/webproject/config

chmod 644 ~/webproject/public/index.html
chmod 600 ~/webproject/private/db.conf
chmod 644 ~/webproject/config/settings.php

# Step 4: Verify करो
ls -lR ~/webproject/

# Step 5: Check करो कि others को कोई sensitive access नहीं है
stat ~/webproject/private/db.conf | grep Access
# परिणाम में "private" दिखना चाहिए "other" के लिए
```

---

### **DAY 9: Common Mistakes & Troubleshooting**

#### ❌ गलती 1: सब कुछ को 777 देना

```bash
# ✗ WRONG (बहुत खतरनाक!)
chmod -R 777 /home/user/
# अब कोई भी कोई भी फाइल delete कर सकता है!

# ✓ CORRECT
chmod 755 ~/myfiles/           # Directories
chmod 644 ~/myfiles/*.txt      # Files
```

#### ❌ गलती 2: Directory को 600 करना

```bash
# ✗ WRONG (अब directory खोल ही नहीं सकते)
chmod 600 ~/documents/
# Result: कोई भी फाइल access नहीं कर सकता, बहु owner भी!

# ✓ CORRECT (directory को execute चाहिए)
chmod 700 ~/documents/  # rwx------ 
chmod 755 ~/documents/  # rwxr-xr-x
```

#### ❌ गलती 3: Script को +x के बिना चलाना

```bash
# ✗ WRONG
./script.sh
# Output: Permission denied

# ✓ CORRECT
chmod +x script.sh
./script.sh
```

#### 🧪 Lab 9.1: Troubleshooting Scenarios

```bash
# Scenario A: "Permission denied" when opening file

# Problem:
cat ~/secret.txt
# Output: Permission denied

# Diagnosis:
ls -l ~/secret.txt
# Output: -rw-r----- root developers 0 May 30 10:00 secret.txt
# Cause: Owner है root, आप developer हो, permission नहीं है

# Solution:
sudo chmod 644 ~/secret.txt  # या
sudo chown yourname ~/secret.txt

# ================================

# Scenario B: Script काम नहीं कर रहा है

# Problem:
./deploy.sh
# Output: Permission denied

# Diagnosis:
ls -l ./deploy.sh
# Output: -rw-r--r-- yourname yourgroup
# Cause: execute permission नहीं है

# Solution:
chmod +x ./deploy.sh

# ================================

# Scenario C: Directory खोल नहीं सकते

# Problem:
cd ~/work
# Output: Permission denied

# Diagnosis:
ls -ld ~/work
# Output: -rwx------ yourname yourgroup
# Wait, यह file permission है, directory नहीं!
ls -ld ~/work
# Output: d--- ------ yourname yourgroup
# Cause: directory को execute permission नहीं है

# Solution:
chmod 755 ~/work
# या कम से कम:
chmod u+x ~/work
```

---

### **DAY 10: Practical Assignments & Mini Project**

#### 📝 Assignment 1: Permission Calculator

```bash
# आपको दिए गए कमांड्स के लिए numeric permission बताएं

# 1. chmod 755 file → क्या permission है?
#    Answer: rwxr-xr-x

# 2. chmod 640 file → क्या permission है?
#    Answer: rw-r-----

# 3. chmod 1777 dir → क्या है?
#    Answer: rwxrwxrwt (Sticky Bit!)

# 4. chmod 4755 script → क्या है?
#    Answer: rwsr-xr-x (SUID!)

# अपने answers ~/assignments/day10_permissions.txt में डालें
```

#### 📝 Assignment 2: Real Scenario - Multi-User Project

```bash
# Scenario: 3-member development team
# Members: alice, bob, charlie
# Project: /home/projects/web-app

# करना:
# 1. Project directory बनाएं (SGID के साथ)
sudo mkdir -p /home/projects/web-app
sudo groupadd web-devs
sudo chown root:web-devs /home/projects/web-app
sudo chmod 2770 /home/projects/web-app

# 2. Members को add करें
sudo usermod -aG web-devs alice
sudo usermod -aG web-devs bob
sudo usermod -aG web-devs charlie

# 3. Subdirectories बनाएं
mkdir src config public private
chmod 770 src config public private

# 4. Config file को secure करें (सिर्फ current user)
echo "DB_PASS=secret" > config/db.conf
chmod 600 config/db.conf

# 5. Public assets
mkdir public/images public/css
chmod 755 public/images public/css
chmod 644 public/images/*
chmod 644 public/css/*

# Verification:
ls -lR /home/projects/web-app/
# सब कुछ web-devs group में होना चाहिए!
```

#### 🎯 Mini Project: File Permission Audit Script

```bash
# ~/mini-project/permission-audit.sh

#!/bin/bash
# Audit करो कि कौन-कौन सी files में risky permissions हैं

echo "=== Permission Audit Report ===" > audit_report.txt
echo "Date: $(date)" >> audit_report.txt
echo "" >> audit_report.txt

# 1. Find world-writable files
echo "RISK: World-writable files:" >> audit_report.txt
find ~ -type f -perm -002 2>/dev/null >> audit_report.txt
echo "" >> audit_report.txt

# 2. Find SUID files
echo "WARNING: SUID files:" >> audit_report.txt
find / -type f -perm -4000 2>/dev/null >> audit_report.txt
echo "" >> audit_report.txt

# 3. Find files with unusual permissions (777)
echo "WARNING: 777 permissions:" >> audit_report.txt
find ~ -type f -perm 777 2>/dev/null >> audit_report.txt

echo "Report saved to audit_report.txt"
cat audit_report.txt
```

---

## 📚 Summary: Permission Quick Reference

```
OCTAL REFERENCE:
0 = ---
1 = --x
2 = -w-
3 = -wx
4 = r--
5 = r-x
6 = rw-
7 = rwx

SPECIAL BITS:
4xxx = SUID (Set User ID)
2xxx = SGID (Set Group ID)
1xxx = Sticky Bit

COMMON PATTERNS:
755  = rwxr-xr-x  (directories, scripts)
644  = rw-r--r--  (text files, documents)
600  = rw-------  (private files)
700  = rwx------  (private directories)
444  = r--r--r--  (read-only)

COMMANDS SUMMARY:
chmod 755 file                    # Set to rwxr-xr-x
chmod u+x file                    # Add execute for user
chmod g-w file                    # Remove write for group
chmod a-x file                    # Remove execute for all
chmod -R 755 directory/           # Recursive
chown owner:group file            # Change owner and group
chown -R owner:group directory/   # Recursive chown
getfacl file                      # View ACLs
setfacl -m u:user:rw file        # Add ACL for user
```

---

## 💡 Interview Preparation

### Q1: chmod 755 क्या करता है?
**Answer**: 
- User को: rwx (read, write, execute) - 7
- Group को: r-x (read, execute) - 5
- Others को: r-x (read, execute) - 5
- यह directories और scripts के लिए standard है

### Q2: SUID क्यों जरूरी है?
**Answer**:
- कुछ programs (जैसे passwd) को admin permissions चाहिए
- लेकिन normal user भी चलाना चाहते हैं
- SUID set करने से program admin के rights से चलता है
- /usr/bin/passwd = -rwsr-xr-x (SUID set है)

### Q3: ACL vs Standard Permissions?
**Answer**:
- Standard permissions: 3 categories (user, group, others)
- ACL: किसी specific user को specific permissions दे सकते हो
- Example: alice को rw, bob को r, others को x - यह ACL से ही बन सकता है

### Q4: Directory को 600 करने का क्या होगा?
**Answer**: 
- Directory को cd करने के लिए execute permission चाहिए
- chmod 600 से no execute होता है
- तो कोई भी उसे open नहीं कर सकता, owner भी नहीं!
- Correct: chmod 700 (rwx------) या chmod 755 (rwxr-xr-x)

### Q5: Sticky Bit कहाँ use होता है?
**Answer**:
- /tmp directory में (chmod 1777)
- अगर आप file create करते हो तो सिर्फ आप delete कर सकते हो
- दूसरा user delete नहीं कर सकता, भले ही directory में write permission हो
- Security के लिए shared directories में उपयोगी है

### Q6: Umask क्या है?
**Answer**:
- Default permission हटाने का तरीका
- New file को 666 (rw-rw-rw-) और directory को 777 मिलते हैं
- Umask से यह subtract होता है
- Typical umask: 0022
  - File: 666 - 022 = 644 (rw-r--r--)
  - Directory: 777 - 022 = 755 (rwxr-xr-x)

### Q7: Recursive chmod करते समय directories और files को अलग कर सकते हो?
**Answer**:
```bash
# सभी को 755 दो
chmod -R 755 ~/myfiles/

# Directories को 755, Files को 644
find ~/myfiles/ -type d -exec chmod 755 {} \;
find ~/myfiles/ -type f -exec chmod 644 {} \;

# या बेहतर:
chmod 755 $(find ~/myfiles/ -type d)
chmod 644 $(find ~/myfiles/ -type f)
```

### Q8: SGID क्या करता है directory के लिए?
**Answer**:
- Directory में नई files/directories automatically same group में जाती हैं
- Example: /project को developers group के साथ SGID
- अब कोई भी /project में file create करे, वह developers group की होगी
- Multi-user projects के लिए बहुत उपयोगी है

---

## ✅ Checklist: आपने क्या सीखा?

- [ ] Permission का मतलब समझ गए (r, w, x)
- [ ] Octal notation (755, 644, 777) को समझ गए
- [ ] Symbolic notation (u+x, g-w) को समझ गए
- [ ] chmod command से permissions बदलना सीख गए
- [ ] chown से owner बदलना सीख गए
- [ ] chgrp से group बदलना सीख गए
- [ ] SUID, SGID, Sticky Bit क्या होते हैं समझ गए
- [ ] ACLs से advanced permissions दे सकते हो
- [ ] Real-world scenarios में permissions लगा सकते हो
- [ ] Troubleshooting कर सकते हो (Permission denied etc.)

---

## 🚀 अगला Phase

Phase 5: **Linux Services & Systemd** (12 दिन)
- Services क्या होते हैं
- systemd क्या है
- systemctl से services control करना
- Service files बनाना
- Logging with journalctl

---

**Happy Learning! 🎓**

> **याद रखें**: Strong permissions, Strong Security!
> Security की शुरुआत File Permissions से होती है।
