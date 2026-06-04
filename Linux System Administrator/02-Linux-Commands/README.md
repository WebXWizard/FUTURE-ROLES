# PHASE 2: Linux Commands - Complete Guide (20 Days)

## 📚 Table of Contents

### Section 1: Navigation Commands (Day 1-2)
### Section 2: File Management Commands (Day 3-4)  
### Section 3: Search Commands (Day 5-6)
### Section 4: Text Processing Commands (Day 7-8)
### Section 5: Compression Commands (Day 9-10)
### Section 6: Package Management (Day 11-15)
### Section 7: Advanced Command Combinations (Day 16-20)

---

# DAY 1-2: NAVIGATION COMMANDS

## 🎓 Theory

### What do navigation commands do?
To move around the filesystem - to explore files and directories.

---

## 1️⃣ Command: `pwd` (Print Working Directory)

### Syntax
```bash
pwd [options]
```

### Examples
```bash
# आपका current directory बताता है
$ pwd
/home/john

# Full physical path दिखाता है (symlinks resolve करके)
$ pwd -P
/var/home/john
```

### Real-world Use Case
```bash
# आप confused हैं कि आप कहां हो
$ pwd
/home/john/Documents/Projects/MyApp

# अब आप जानते हो
# अगला command run करना सुरक्षित है
$ rm -rf ../*
# Wait! डेलीट करने से पहले pwd से confirm करो!
```

### Interview Questions
**Q: pwd के output में symlink नहीं दिखता, क्या करोगे?**
```
A: pwd -P use करो
   यह physical path दिखाता है, symlinks को resolve करके
```

### Practice Tasks
```bash
1. pwd चलाओ
2. pwd -P चलाओ
3. अंतर देखो
4. अपनी current directory का path note करो
```

---

## 2️⃣ Command: `cd` (Change Directory)

### Syntax
```bash
cd [directory_path]
```

### Examples
```bash
# Home directory में जाना
$ cd ~
$ cd
$ cd $HOME

# Parent directory में जाना
$ cd ..

# Absolute path का use करके
$ cd /usr/bin
$ pwd
/usr/bin

# Relative path का use करके
$ cd ../documents
$ cd ./subfolder

# पिछली directory में जाना
$ cd -

# Root directory में जाना
$ cd /
```

### Real-world Use Case
```bash
# Web developer को अलग-अलग project folders में जाना पड़ता है

$ cd ~/projects/frontend
# Frontend project पर काम करता है

$ cd -
# Back to previous project

$ cd ~/projects/backend
# Backend project में जाता है

$ pwd
/home/john/projects/backend
```

### Interview Questions
**Q: cd के बाद command नहीं चल रहा है?**
```
A: Possible causes:
1. Directory exist नहीं करती - ls से check करो
2. Permission नहीं है - ls -ld से permissions देखो
3. Typo है नाम में - सावधानी से type करो
```

### Practice Tasks
```bash
1. Home directory में जाओ: cd ~
2. Root में जाओ: cd /
3. पिछली directory में जाओ: cd -
4. /etc जाओ फिर /var जाओ फिर previous में जाओ
5. Nested directory structure create करो और navigate करो
```

---

## 3️⃣ Command: `ls` (List Directory Contents)

### Syntax
```bash
ls [options] [directory_or_file]
```

### Options विस्तार से

| Option | Meaning | Example |
|--------|---------|---------|
| `-l` | Long format (details) | `ls -l` |
| `-a` | सभी files (hidden भी) | `ls -a` |
| `-h` | Human readable (sizes) | `ls -lh` |
| `-r` | Reverse order | `ls -r` |
| `-R` | Recursive (subdirs भी) | `ls -R` |
| `-t` | Sort by modification time | `ls -t` |
| `-S` | Sort by size | `ls -S` |
| `-d` | Directories को files जैसे show करो | `ls -d */` |

### Examples

#### Basic ls
```bash
$ ls
Desktop  Documents  Downloads  Music  Pictures  Videos

$ ls /home
john  alice  bob
```

#### ls -l (Long format)
```bash
$ ls -l
total 40
drwxr-xr-x 2 john john 4096 May 20 10:30 Desktop
drwxr-xr-x 2 john john 4096 May 15 14:20 Documents
-rw-r--r-- 1 john john 2048 May 18 09:15 file.txt

# Format:
# drwxr-xr-x = Permissions (first char: - for file, d for directory)
# 2 = Number of hard links
# john john = Owner and Group
# 4096 = Size in bytes
# May 20 10:30 = Modification date and time
# Desktop = Filename
```

#### ls -lh (Human readable size)
```bash
$ ls -lh
total 1.2M
drwxr-xr-x 2 john john 4.0K May 20 10:30 Desktop
-rw-r--r-- 1 john john 2.0M May 18 09:15 video.mp4

# Sizes अब readable हैं: K, M, G
```

#### ls -la (सभी files including hidden)
```bash
$ ls -la
total 120
drwxr-xr-x 10 john john 4096 May 20 10:30 .
drwxr-xr-x  3 root root 4096 May 10 08:00 ..
-rw-r--r--  1 john john  220 May 10 08:00 .bash_logout
-rw-r--r--  1 john john 3771 May 10 08:00 .bashrc
-rw-r--r--  1 john john  807 May 10 08:00 .profile
drwxr-xr-x  2 john john 4096 May 20 10:30 Desktop

# Files जो . से start होती हैं वो hidden होती हैं!
```

#### ls -R (Recursive - पूरी tree दिखाओ)
```bash
$ ls -R ~/Documents
.:
file1.txt  subdir/

./subdir:
file2.txt  nested/

./subdir/nested:
file3.txt
```

#### ls -lS (Size के हिसाब से sort)
```bash
$ ls -lS
-rw-r--r-- 1 john john  50M May 15 10:00 video.mp4
-rw-r--r-- 1 john john 5.2M May 18 09:15 image.iso
-rw-r--r-- 1 john john  120K May 20 11:30 document.pdf
-rw-r--r-- 1 john john   5K May 20 12:00 notes.txt
```

### Real-world Use Cases

```bash
# Use Case 1: Disk space को check करना
$ ls -lhS /var/log
# सबसे बड़ी log files देख सकते हो

# Use Case 2: Hidden files को find करना
$ ls -la ~/.ssh
# SSH keys को देख सकते हो

# Use Case 3: Directory structure को समझना
$ ls -R /etc | head -50
# पूरी directory structure देख सकते हो

# Use Case 4: Recent changes को देखना
$ ls -lt
# हाल ही की modified files सबसे ऊपर

# Use Case 5: Production में file permissions check करना
$ ls -l /var/www/html
# Web server files की permissions देख सकते हो
```

### Interview Questions

**Q: ls -la में . और .. क्या हैं?**
```
A: 
. = Current directory को refer करता है
.. = Parent directory को refer करता है

Use:
$ cd .
$ pwd
/home/john  (same directory)

$ cd ..
$ pwd
/home  (parent directory)
```

**Q: ls के output में @ या + क्या मतलब है?**
```
A: 
@ = File में extended attributes हैं (ACLs, etc)
+ = File को SELinux context है
. = File को ACLs हैं

Example:
-rw-r--r--+ 1 john john 1024 May 20 10:30 file.txt
           ^ यह + है
```

### Practice Tasks
```bash
1. ls विभिन्न directories में चलाओ
2. ls -la से hidden files को देखो
3. ls -lh से file sizes को समझो
4. ls -lS से largest files देखो
5. ls -lt से recent files देखो
6. Combine करो multiple options: ls -lahSt
```

---

## 4️⃣ Command: `mkdir` (Make Directory)

### Syntax
```bash
mkdir [options] directory_name
```

### Options
```bash
-p    # Parent directories को भी बनाता है
-m    # Permissions set करता है
```

### Examples
```bash
# Simple directory create करना
$ mkdir mydir
$ ls
mydir

# Multiple directories एक साथ
$ mkdir dir1 dir2 dir3

# Parent directories के साथ (parent नहीं होंगे तो बनेंगे)
$ mkdir -p /home/john/projects/python/app
# यह सभी intermediate directories create करेगा

# Permissions के साथ
$ mkdir -m 755 publicdir
$ mkdir -m 700 privatedir
```

### Real-world Use Case
```bash
# Server setup के समय

# Project structure बनाते हो
$ mkdir -p ~/myapp/{src,tests,docs,config,logs}

# Check करो
$ ls -la ~/myapp/
drwxr-xr-x 7 john john 4096 May 20 10:30 myapp
drwxr-xr-x 2 john john 4096 May 20 10:30 config
drwxr-xr-x 2 john john 4096 May 20 10:30 docs
drwxr-xr-x 2 john john 4096 May 20 10:30 logs
drwxr-xr-x 2 john john 4096 May 20 10:30 src
drwxr-xr-x 2 john john 4096 May 20 10:30 tests
```

### Practice Tasks
```bash
1. simple directory create करो
2. nested directories बनाओ
3. permissions के साथ directory बनाओ
```

---

# DAY 3-4: FILE MANAGEMENT COMMANDS

## 1️⃣ Command: `touch`

### Purpose: Files को create या update करना

```bash
# File create करना
$ touch myfile.txt
$ ls -l myfile.txt
-rw-r--r-- 1 john john 0 May 20 10:30 myfile.txt

# Multiple files create करना
$ touch file1.txt file2.txt file3.txt

# File का modification time को update करना
$ touch myfile.txt
# अब modification time current है

# Future date के साथ
$ touch -d "2025-12-31 10:00:00" myfile.txt
```

---

## 2️⃣ Command: `cp` (Copy)

### Syntax
```bash
cp [options] source destination
```

### Key Options
```bash
-r    # Recursive (directories के लिए)
-i    # Interactive (overwrite से पहले पूछो)
-p    # Preserve permissions and timestamps
-v    # Verbose (क्या copy हो रहा है दिखाओ)
```

### Examples
```bash
# File को copy करना
$ cp file.txt file_copy.txt

# File को दूसरी directory में copy करना
$ cp file.txt ~/Documents/

# Directory को copy करना (सभी files के साथ)
$ cp -r mydir mydir_backup

# Permissions को maintain करके copy करना
$ cp -p file.txt backup_file.txt

# Verbose mode - क्या copy हो रहा है देखना
$ cp -v *.txt ~/Documents/
'file1.txt' -> '/home/john/Documents/file1.txt'
'file2.txt' -> '/home/john/Documents/file2.txt'

# Overwrite से पहले ask करना
$ cp -i file.txt existing_file.txt
cp: overwrite 'existing_file.txt'? y
```

### Real-world Use Case
```bash
# Configuration file का backup लेना
$ cp -p /etc/nginx/nginx.conf /etc/nginx/nginx.conf.backup

# पूरी directory को backup करना
$ cp -r ~/myapp ~/myapp.backup.2024

# Multiple files को copy करना
$ cp -r src/ tests/ docs/ ~/backup/
```

---

## 3️⃣ Command: `mv` (Move/Rename)

### Syntax
```bash
mv [options] source destination
```

### Examples
```bash
# File को rename करना
$ mv oldname.txt newname.txt

# File को दूसरी directory में move करना
$ mv file.txt ~/Documents/

# Directory को move करना
$ mv mydir ~/projects/

# Multiple files को move करना
$ mv *.txt ~/Documents/

# Verbose mode
$ mv -v file1 file2 ~/backup/
'file1' -> '/home/john/backup/file1'
'file2' -> '/home/john/backup/file2'
```

### Real-world Use Case
```bash
# Production में logs को rotate करना
$ mv /var/log/app.log /var/log/app.log.old
$ touch /var/log/app.log

# Temporary files को clean करना
$ mv /tmp/tempfiles ~/archive/
```

---

## 4️⃣ Command: `rm` (Remove)

### ⚠️ WARNING: यह command बहुत powerful है, सावधानी से use करो!

### Syntax
```bash
rm [options] file_or_directory
```

### Options
```bash
-i    # Interactive (delete से पहले पूछो) ✅ ALWAYS USE
-r    # Recursive (directories के लिए)
-f    # Force (बिना पूछे delete करो) ⚠️ DANGEROUS
-v    # Verbose
```

### Examples
```bash
# Single file को delete करना
$ rm file.txt

# Interactive mode - सुरक्षित तरीका ✅
$ rm -i file.txt
remove regular file 'file.txt'? y

# Directory और सभी files को delete करना
$ rm -r mydir/

# Multiple files को delete करना
$ rm file1.txt file2.txt file3.txt

# Verbose mode (क्या delete हो रहा है देखना)
$ rm -v file*.txt
removed 'file1.txt'
removed 'file2.txt'
```

### ⚠️ DANGEROUS Commands (कभी मत करो!)

```bash
❌ NEVER: rm -rf /
❌ NEVER: rm -rf /*
❌ NEVER: rm -rf ~/.
❌ NEVER: sudo rm -rf /home/*/
```

### Real-world Scenario
```bash
# Disk space free करने के लिए पुरानी files delete करना
$ cd /var/log
$ rm -i *.old
remove 'syslog.old'? y
remove 'auth.log.old'? y

# Temporary files को clean करना
$ cd /tmp
$ rm -rf *old*

# Production में carefully!
$ ls -la # पहले check करो क्या है
$ rm -i old_backup_files  # interactive mode
```

---

## 5️⃣ Command: `cat` (Concatenate/View)

### Purpose: File का content देखना

```bash
# File को देखना
$ cat file.txt
Hello World!

# Multiple files को देखना
$ cat file1.txt file2.txt

# Content को दूसरी file में copy करना
$ cat file1.txt > newfile.txt

# Content को existing file में append करना
$ cat file1.txt >> file2.txt

# Line numbers के साथ
$ cat -n file.txt
     1	Line 1
     2	Line 2
     3	Line 3

# Empty lines को skip करना
$ cat -s file.txt
```

### Real-world Use Case
```bash
# Configuration file को check करना
$ cat /etc/hostname
my-server

# Log files को देखना
$ cat /var/log/syslog | head -20

# File को combine करना
$ cat part1.bin part2.bin > complete.bin
```

---

## 6️⃣ Command: `less` / `more`

### Purpose: Large files को efficiently देखना

```bash
# less का use करो (better than more)
$ less /var/log/syslog

# Navigation:
# 'j' = down line
# 'k' = up line
# 'G' = end of file
# 'g' = beginning of file
# '/search_term' = search करना
# 'q' = quit करना

# Commands
$ less +G /var/log/syslog  # End से खोलो
$ less +/ERROR /var/log/syslog  # ERROR keyword को search करके खोलो
```

---

## HANDS-ON LAB 2.1: File Management Practice

```bash
# Lab Objective: अलग-अलग file operations को practice करना

# Step 1: Working directory में जाओ
$ cd ~/

# Step 2: Test directory create करो
$ mkdir -p test/data
$ cd test

# Step 3: Files create करो
$ touch file1.txt file2.txt file3.txt

# Step 4: Files को देखो
$ ls -la

# Step 5: Content add करो
$ echo "This is file 1" > file1.txt
$ echo "This is file 2" > file2.txt

# Step 6: Files को देखो
$ cat file1.txt
$ cat file2.txt

# Step 7: Copy करो
$ cp file1.txt file1_backup.txt
$ ls -la

# Step 8: Rename करो
$ mv file2.txt file2_renamed.txt
$ ls -la

# Step 9: Delete करो
$ rm -i file3.txt
remove regular file 'file3.txt'? y

# Step 10: Result check करो
$ ls -la
```

---

## INTERVIEW QUESTIONS - SECTION 1 & 2

**Q1: pwd, cd, ls में क्या अंतर है?**
```
pwd: आपकी current location बताता है
cd: नई location पर जाता है
ls: Current location की files/directories दिखाता है
```

**Q2: rm -rf का use करते हुए file accidentally delete हो गई?**
```
A: Linux में deleted files को recover करना बहुत मुश्किल है।
Prevention:
- rm -i का always use करो (interactive)
- पहले ls से check करो
- Important files का regular backup रखो
- Production में बहुत सावधान रहो
```

**Q3: cp और mv में क्या अंतर है?**
```
cp: File को copy करता है (original बनी रहती है)
mv: File को move करता है (नई location पर जाती है)
   या rename करता है

Memory में:
cp: source और destination दोनों exist करती हैं
mv: source हटती है destination पर जाती है
```

---

# DAY 5-6: SEARCH COMMANDS

## 1️⃣ Command: `find`

### Purpose: Files को search करना (filename, size, type, date based)

### Syntax
```bash
find [path] [options] [expression]
```

### Options

| Option | Meaning |
|--------|---------|
| `-name` | Filename के basis पर |
| `-size` | File size के basis पर |
| `-type` | File type के basis पर (f=file, d=directory) |
| `-mtime` | Modified time के basis पर |
| `-user` | Owner के basis पर |
| `-perm` | Permissions के basis पर |

### Examples

```bash
# Current directory में सभी .txt files
$ find . -name "*.txt"
./file1.txt
./folder/file2.txt

# Specific directory में search
$ find /home -name "*.log"

# Files को find करो (directories नहीं)
$ find . -type f -name "*.txt"

# Directories को find करो
$ find . -type d -name "test*"

# Size के basis पर
$ find . -size +10M  # 10MB से बड़ी files
$ find . -size -1M   # 1MB से छोटी files
$ find . -size 10M   # Exactly 10MB

# Modified time के basis पर
$ find . -mtime -7   # पिछले 7 दिन में modified
$ find . -mtime +7   # 7 दिन से पहले modified
$ find . -mtime 7    # Exactly 7 days ago

# Owner के basis पर
$ find . -user john

# Permissions के basis पर
$ find . -perm 644   # Exactly 644 permissions

# Case-insensitive search
$ find . -iname "*.TXT"  # .TXT, .txt, .Txt सब match करेगा
```

### Real-world Use Cases

```bash
# Production में बड़ी log files को find करना
$ find /var/log -name "*.log" -size +100M

# 30 दिन से पहले की backup files को delete करना
$ find /backup -name "*.backup" -mtime +30 -type f

# Permission issues को find करना
$ find /home -type f -perm 777  # World-writable files (security risk!)

# Specific user के सभी files
$ find /home -user john -type f

# Development machine में .git directories को find करना
$ find . -type d -name ".git"

# Empty files को find करना
$ find . -type f -empty
```

---

## 2️⃣ Command: `locate`

### Purpose: Database से quickly files को search करना

```bash
# locate का use करना
$ locate myfile.txt
/home/john/myfile.txt
/var/log/myfile.txt.old

# Pattern का use करना
$ locate "*.log"

# Database को update करना (नई files के लिए)
$ sudo updatedb

# Count करना कितनी files match हैं
$ locate -c "*.log"
42

# Basename के basis पर (पूरा path नहीं)
$ locate -b "myfile"
```

### फायदे और नुकसान
```bash
find vs locate:

find:
✅ Real-time search
✅ Complex filtering
❌ Slow (पूरी filesystem को scan करता है)

locate:
✅ Very fast (database से)
❌ Not real-time
❌ Database outdated हो सकता है
```

---

## 3️⃣ Command: `grep`

### Purpose: Text content के within files को search करना

### Syntax
```bash
grep [options] pattern [file(s)]
```

### Options
```bash
-r    # Recursive (subdirectories में भी search)
-i    # Case-insensitive
-v    # Invert match (जो pattern से match न करो)
-c    # Count of matching lines
-n    # Line numbers
-l    # Just list filenames
```

### Examples

```bash
# Simple search
$ grep "error" /var/log/syslog
2024-05-20 10:30:45 ERROR: Database connection failed

# Multiple files में search
$ grep "error" /var/log/*.log

# Case-insensitive
$ grep -i "ERROR" /var/log/syslog

# Line numbers के साथ
$ grep -n "error" /var/log/syslog
125: ERROR: Database connection failed
340: WARNING: Error in module

# Count करना
$ grep -c "error" /var/log/syslog
245

# Invert match (error नहीं हैं)
$ grep -v "error" /var/log/syslog | head -5

# Recursive (सभी subdirectories में)
$ grep -r "TODO" .

# File के list के साथ
$ grep -l "database" *.py
app.py
config.py
utils.py

# Regular expressions का use
$ grep "^ERROR" /var/log/syslog  # Lines जो ERROR से start हों
$ grep "file$" /var/log/syslog   # Lines जो 'file' पर end हों
$ grep "err.*" /var/log/syslog   # 'err' के बाद कुछ भी हो
```

### Real-world Use Cases

```bash
# Log files में errors को find करना
$ grep -i "error\|exception\|failed" /var/log/app.log | wc -l

# Configuration में specific setting को find करना
$ grep "database_host" /etc/app/config.yaml

# Source code में TODO comments को find करना
$ grep -r "TODO\|FIXME" src/

# सभी errors को grep और उन्हें unique count करना
$ grep "error" /var/log/syslog | sort | uniq -c | sort -rn

# Specific user की SSH login attempts
$ grep "sshd" /var/log/auth.log | grep "Failed"
```

---

## HANDS-ON LAB 2.2: Search Commands Practice

```bash
# Lab: Search operations को practice करना

# Step 1: Test files create करो
$ cd ~/test
$ echo "error in line 1" > file1.txt
$ echo "ERROR in line 2" >> file1.txt
$ echo "Warning in file2" > file2.txt
$ echo "debug message" >> file2.txt

# Step 2: find से .txt files को search करो
$ find . -name "*.txt"

# Step 3: grep से "error" को search करो
$ grep -i "error" file1.txt

# Step 4: grep से line numbers के साथ
$ grep -in "error" file1.txt

# Step 5: Recursive search करो
$ grep -r "message" .

# Step 6: Count करो कितने lines match करती हैं
$ grep -c "error" file1.txt
```

---

# DAY 7-8: TEXT PROCESSING COMMANDS

## 1️⃣ Command: `sed` (Stream Editor)

### Purpose: Text को modify करना (replace, delete, insert)

### Syntax
```bash
sed [options] 'command' [file]

Commands:
s = substitute/replace
d = delete
a = append
i = insert
p = print
```

### Examples

```bash
# Replace करना (पहली occurrence)
$ echo "hello world hello" | sed 's/hello/hi/'
hi world hello

# Replace करना (सभी occurrences)
$ echo "hello world hello" | sed 's/hello/hi/g'
hi world hi

# Line को delete करना
$ sed '1d' file.txt  # First line को delete करो
$ sed '1,3d' file.txt  # Lines 1-3 को delete करो
$ sed '/pattern/d' file.txt  # Pattern matching line को delete करो

# Lines को print करना
$ sed -n '5,10p' file.txt  # Lines 5-10 print करो

# Append करना
$ sed '5a\ New line here' file.txt
# Line 5 के बाद "New line here" add करता है

# File को directly modify करना
$ sed -i 's/old/new/g' file.txt
# -i flag से file को modify करता है (backup रखो!)
$ sed -i.bak 's/old/new/g' file.txt  # .bak backup रखेगा
```

### Real-world Use Cases

```bash
# Configuration file में values को change करना
$ sed -i 's/debug=true/debug=false/g' config.ini

# Log files से specific lines को remove करना
$ sed '/ERROR/d' app.log > app_clean.log

# CSV file को process करना
$ sed 's/,/ | /g' data.csv  # Commas को pipes में change करना

# IP address को find करना
$ sed -n '/192.168.1.1/p' /var/log/syslog

# Line endings को change करना
$ sed 's/$/\r/' file.txt  # DOS line endings add करना
```

---

## 2️⃣ Command: `awk`

### Purpose: Structured data (columns) को process करना

### Syntax
```bash
awk [options] 'pattern { action }' [file]
```

### Examples

```bash
# Columns को print करना
$ echo "John 25 Engineer" | awk '{print $1}'
John

$ echo "John 25 Engineer" | awk '{print $3, $1}'
Engineer John

# Column को manipulate करना
$ echo "John 25 Engineer" | awk '{print $1 ": " $2}'
John: 25

# Specific column को process करना
$ ps aux | awk '{print $1, $2}' 
# Username (column 1) और PID (column 2) दिखाएगा

# Header को skip करना और processing करना
$ awk 'NR > 1 {print $1}' users.txt
# पहली line (header) को छोड़कर बाकी lines को process करता है

# Calculation करना
$ echo "100 200 300" | awk '{print $1 + $2 + $3}'
600

# Conditional logic
$ awk '$2 > 25 {print $1}' users.txt
# Age (column 2) 25 से ज्यादा वालों को print करो

# BEGIN और END blocks
$ awk 'BEGIN {print "Starting..."} {print $1} END {print "Done!"}' file.txt

# NR (Number of Records) का use
$ awk 'NR == 5 {print}' file.txt  # 5th line print करो
$ awk 'NR >= 10 && NR <= 20 {print}' file.txt  # Lines 10-20
```

### Real-world Use Cases

```bash
# Apache log से specific column को extract करना
$ awk '{print $1}' /var/log/apache2/access.log  # IP addresses

# Disk usage को summary करना
$ df -h | awk '{print $1, $5}' | grep -v "Filesystem"
# Filesystem और usage percentage

# CSV में specific columns को extract करना
$ awk -F',' '{print $2, $3}' data.csv  # Columns 2 और 3
# -F option field separator को define करता है

# Process size को check करना
$ ps aux | awk '$6 > 100000 {print $1, $6/1024 " MB"}'
# 100MB से बड़ी processes को MB में दिखाएगा
```

---

## 3️⃣ Command: `cut`

### Purpose: Specific columns को extract करना

### Examples

```bash
# Column को extract करना (character positions)
$ echo "Hello World" | cut -c 1-5
Hello

# Delimiter के साथ (जैसे CSV)
$ cat users.csv | cut -d',' -f1,3
# Comma-delimited file में column 1 और 3

# Colon-delimited (जैसे /etc/passwd)
$ cut -d':' -f1,3 /etc/passwd
# Username और UID
```

---

## HANDS-ON LAB 2.3: Text Processing Practice

```bash
# Create test file
$ cat > data.txt << EOF
John 25 Engineer 5000
Alice 30 Manager 8000
Bob 22 Intern 2000
EOF

# sed से replace करना
$ sed 's/Engineer/Senior Engineer/g' data.txt

# awk से specific columns print करना
$ awk '{print $1, $4}' data.txt

# awk से calculation करना
$ awk '{sum += $4} END {print "Total Salary: " sum}' data.txt

# cut से columns extract करना
$ cut -d' ' -f1,2 data.txt
```

---

# DAY 9-10: COMPRESSION COMMANDS

## 1️⃣ Command: `tar`

### Purpose: Files को bundle/archive करना

### Syntax
```bash
tar [options] filename.tar [files/directories]
```

### Options
```bash
c = create archive
x = extract
f = file (archive filename)
v = verbose
z = gzip compression
j = bzip2 compression
```

### Examples

```bash
# Create करना
$ tar -cvf archive.tar file1.txt file2.txt
$ tar -cvf archive.tar mydir/

# Extract करना
$ tar -xvf archive.tar

# gzip के साथ (compressed)
$ tar -cvzf archive.tar.gz mydir/
$ tar -xvzf archive.tar.gz

# bzip2 के साथ
$ tar -cvjf archive.tar.bz2 mydir/

# List करना (extract किए बिना)
$ tar -tvf archive.tar
```

### Real-world Use Case
```bash
# Backup लेना
$ tar -cvzf backup_$(date +%Y%m%d).tar.gz ~/myapp/

# Distribution के लिए
$ tar -cvzf myapp-1.0.tar.gz myapp/
```

---

## 2️⃣ Command: `gzip`

### Purpose: Individual files को compress करना

```bash
# Compress करना
$ gzip file.txt
# Creates: file.txt.gz (original delete हो जाती है)

# Decompress करना
$ gunzip file.txt.gz
# या
$ gzip -d file.txt.gz

# Compression level
$ gzip -9 file.txt  # Maximum compression
$ gzip -1 file.txt  # Minimum compression (fast)

# Original file को keep करना
$ gzip -k file.txt
# file.txt और file.txt.gz दोनों रहेंगे
```

---

## 3️⃣ Command: `zip`

### Purpose: Files को zip करना (Windows compatible)

```bash
# Zip file create करना
$ zip archive.zip file1.txt file2.txt

# Directory को zip करना
$ zip -r archive.zip mydir/

# Unzip करना
$ unzip archive.zip

# List करना
$ unzip -l archive.zip

# Password के साथ
$ zip -P password archive.zip file.txt
$ unzip -P password archive.zip
```

---

## HANDS-ON LAB 2.4: Compression Practice

```bash
# Create test files
$ touch file1.txt file2.txt file3.txt
$ echo "This is a large file" > largefile.txt

# tar create करना
$ tar -cvf myarchive.tar file1.txt file2.txt file3.txt

# Compressed tar create करना
$ tar -cvzf myarchive.tar.gz file1.txt file2.txt file3.txt

# Extract करना
$ tar -xvzf myarchive.tar.gz

# zip create करना
$ zip myarchive.zip file1.txt file2.txt file3.txt

# gzip से compress करना
$ gzip largefile.txt

# Sizes को compare करना
$ ls -lh file*.txt largefile.txt*
```

---

# DAY 11-15: PACKAGE MANAGEMENT

## Ubuntu/Debian (apt)

### Commands

```bash
# Update package list
$ sudo apt update

# Upgrade packages
$ sudo apt upgrade

# Install करना
$ sudo apt install package_name

# Multiple packages install करना
$ sudo apt install package1 package2 package3

# Remove करना
$ sudo apt remove package_name

# Complete remove (configuration भी)
$ sudo apt purge package_name

# Search करना
$ apt search package_name

# Information देखना
$ apt info package_name

# Clean cache
$ sudo apt clean
$ sudo apt autoclean
```

### Real-world Examples

```bash
# Web server install करना
$ sudo apt update
$ sudo apt install nginx

# Programming language install करना
$ sudo apt install python3 python3-pip

# Development tools
$ sudo apt install build-essential git curl wget
```

---

## CentOS/RHEL (yum/dnf)

### Commands

```bash
# Update
$ sudo yum update

# Install
$ sudo yum install package_name

# Remove
$ sudo yum remove package_name

# Search
$ sudo yum search package_name

# Clean
$ sudo yum clean all
```

---

## All Phases Overview

मैंने आपके लिए एक **Complete Linux System Administrator Learning Roadmap** बनाया है। अब मैं सभी remaining phases की overview दूंगा:

---

