# Phase 09: Shell Scripting - Bash (25 Days)

> The core of Linux automation is shell scripting. Learn 50 scripts from beginner to production-level. This is the most important phase for real-world work!

**Phase Duration**: 25 days  
**Scripts**: 50 (20 beginner, 20 intermediate, 10 advanced)

---

## 📋 What You'll Learn

```
├── Bash Basics (shebang, variables, echo)
├── Variables और Data Types
├── Input/Output (read, echo, printf)
├── Arithmetic और Conditions
├── Loops (for, while, until)
├── Functions और Parameters
├── Arrays
├── String Manipulation
├── File Operations
├── Text Processing (grep, sed, awk)
├── Regular Expressions
├── Error Handling
├── Debugging
├── Advanced Topics (pipes, redirects)
└── Production-ready Scripts (20+ scripts)
```

---

## 🗓️ Day-by-Day (संक्षेप में)

### **DAY 1-2: Basics**

```bash
#!/bin/bash
# Script 1: Hello World
echo "Hello, Linux Admin!"

# Script 2: Variables
name="Ali"
age=25
echo "Name: $name, Age: $age"

# Script 3: Read input
read -p "Enter your name: " input_name
echo "Hello, $input_name"

# Script 4: Comments
# यह एक comment है
: '
Multi-line comment
बहुत जानकारी
'
```

---

### **DAY 3-4: Arithmetic और Conditions**

```bash
# Script 5: Arithmetic
num1=10
num2=20
sum=$((num1 + num2))
echo "Sum: $sum"

# Script 6: If condition
age=18
if [ $age -ge 18 ]; then
    echo "Adult"
else
    echo "Minor"
fi

# Script 7: String comparison
str1="hello"
str2="hello"
if [ "$str1" = "$str2" ]; then
    echo "Equal"
fi

# Script 8: Multiple conditions
if [ $age -ge 18 ] && [ $age -le 65 ]; then
    echo "Working age"
fi
```

---

### **DAY 5-7: Loops**

```bash
# Script 9: For loop (C-style)
for ((i=1; i<=5; i++)); do
    echo "Number: $i"
done

# Script 10: For loop (list)
for color in red blue green; do
    echo "Color: $color"
done

# Script 11: While loop
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done

# Script 12: Until loop
counter=1
until [ $counter -gt 5 ]; do
    echo "Counter: $counter"
    ((counter++))
done

# Script 13: Break and Continue
for i in {1..10}; do
    if [ $i -eq 3 ]; then
        continue
    fi
    if [ $i -eq 8 ]; then
        break
    fi
    echo $i
done
```

---

### **DAY 8-10: Functions**

```bash
# Script 14: Simple function
greet() {
    echo "Hello from function!"
}
greet

# Script 15: Function with parameters
add() {
    local a=$1
    local b=$2
    local sum=$((a + b))
    echo $sum
}
result=$(add 5 3)
echo "Result: $result"

# Script 16: Function with return
is_even() {
    [ $((($1) % 2)) -eq 0 ] && return 0 || return 1
}
if is_even 4; then
    echo "Even"
else
    echo "Odd"
fi

# Script 17: Advanced function
process_file() {
    local file=$1
    local action=$2
    
    if [ ! -f "$file" ]; then
        echo "File not found"
        return 1
    fi
    
    case $action in
        count) wc -l "$file" ;;
        size) ls -lh "$file" | awk '{print $5}' ;;
        *) echo "Unknown action" ;;
    esac
}
```

---

### **DAY 11-13: Arrays**

```bash
# Script 18: Basic array
arr=(apple banana cherry)
echo ${arr[0]}          # apple
echo ${arr[@]}          # सभी elements
echo ${#arr[@]}         # Length

# Script 19: Array operations
arr+=("date")           # Add element
for item in "${arr[@]}"; do
    echo "$item"
done

# Script 20: Associative arrays
declare -A config
config[host]="localhost"
config[port]="8080"
config[user]="admin"
echo ${config[host]}
```

---

### **DAY 14-16: String Manipulation**

```bash
# Script 21: Substring
str="Hello World"
echo ${str:0:5}         # Hello
echo ${str:6}           # World
echo ${str#*o}          # Remove prefix

# Script 22: Replace
echo ${str/World/Linux} # Hello Linux

# Script 23: Length
echo ${#str}            # Length

# Script 24: Case conversion
echo ${str^^}           # Uppercase
echo ${str,,}           # Lowercase
```

---

### **DAY 17-19: File Operations**

```bash
# Script 25: File testing
if [ -f "file.txt" ]; then
    echo "File exists"
fi

[ -d "/path" ] && echo "Directory exists"
[ -r "file.txt" ] && echo "Readable"
[ -w "file.txt" ] && echo "Writable"
[ -x "script.sh" ] && echo "Executable"

# Script 26: Reading file
while IFS= read -r line; do
    echo "Line: $line"
done < "input.txt"

# Script 27: File processing
#!/bin/bash
# Backup script
SOURCE="/home/user/documents"
BACKUP="/backups/documents_$(date +%Y%m%d).tar.gz"
tar czf "$BACKUP" "$SOURCE"
echo "Backup completed: $BACKUP"

# Script 28: Monitoring logs
tail -f /var/log/syslog | grep ERROR | while read line; do
    echo "ERROR: $line"
    # Send alert, etc.
done
```

---

### **DAY 20-22: Text Processing**

```bash
# Script 29: Using grep, sed, awk
# Process CSV
awk -F',' '{print $1, $3}' data.csv

# Extract specific lines
sed -n '5,10p' file.txt

# Replace text
sed 's/old/new/g' file.txt > new_file.txt

# Script 30: Complex text processing
#!/bin/bash
# Log analyzer
log_file="/var/log/auth.log"
grep "Failed password" "$log_file" | \
    awk '{print $NF}' | \
    sort | uniq -c | \
    sort -rn | \
    head -10
```

---

### **DAY 23-25: Production Scripts**

```bash
# Script 31: System monitoring
#!/bin/bash
CPU=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}')
MEM=$(free | grep Mem | awk '{print ($3/$2) * 100.0}')
if (( $(echo "$CPU > 80" | bc -l) )); then
    echo "HIGH CPU: $CPU%"
fi
if (( $(echo "$MEM > 80" | bc -l) )); then
    echo "HIGH MEMORY: $MEM%"
fi

# Script 32: Automated backup
#!/bin/bash
BACKUP_DIR="/backups"
SOURCE_DIR="/important/data"
RETENTION_DAYS=7

# Create backup
BACKUP_FILE="$BACKUP_DIR/backup_$(date +%Y%m%d_%H%M%S).tar.gz"
tar czf "$BACKUP_FILE" "$SOURCE_DIR"

# Delete old backups
find "$BACKUP_DIR" -type f -name "backup_*.tar.gz" -mtime +$RETENTION_DAYS -delete

echo "Backup completed successfully"

# Script 33: Deployment script
#!/bin/bash
APP_DIR="/opt/myapp"
GIT_REPO="https://github.com/user/repo.git"
SERVICE_NAME="myapp"

cd "$APP_DIR"
git pull origin main
npm install
npm run build
sudo systemctl restart "$SERVICE_NAME"
echo "Deployment completed"

# Script 34: Health check
#!/bin/bash
# Check multiple services
services=("ssh" "apache2" "mysql")
for service in "${services[@]}"; do
    if systemctl is-active "$service" &>/dev/null; then
        echo "$service is running ✓"
    else
        echo "$service is DOWN ✗"
        sudo systemctl start "$service"
    fi
done

# Script 35: Interactive menu
#!/bin/bash
while true; do
    echo "=== System Admin Menu ==="
    echo "1. Check disk usage"
    echo "2. Check memory"
    echo "3. List users"
    echo "4. Exit"
    read -p "Choose: " choice
    
    case $choice in
        1) df -h ;;
        2) free -h ;;
        3) cut -d: -f1 /etc/passwd ;;
        4) break ;;
    esac
done
```

---

## 💡 Script Ideas (50 Total)

**Beginner (20):**
1. Hello World
2. Variables
3. Input reading
4. Arithmetic
5. If/else
6. For loop
7. While loop
8. Function basics
9. Array basics
10. String operations
... (10 more basic scripts)

**Intermediate (20):**
1. File operations
2. Text processing (grep, sed, awk)
3. Error handling
4. User input validation
5. Log analysis
6. Monitoring script
7. Backup automation
8. Deployment helper
9. Database backup
10. Report generation
... (10 more intermediate scripts)

**Advanced (10):**
1. Complete monitoring system
2. Automated deployment pipeline
3. Health check with alerting
4. Load balancer health check
5. Database replication monitor
6. Multi-service dependency checker
7. Capacity planning script
8. Performance analyzer
9. Incident response automation
10. Infrastructure provisioning helper

---

## ✅ Interview Questions

**Q: Bash में variable define करते समय space नहीं होनी चाहिए क्यों?**
- `name=value` = correct
- `name = value` = bash command नहीं समझेगा, "name" को command मानेगा

**Q: $() vs backticks (``)?**
- दोनों command substitution करते हैं, पर $() नेस्टिंग के लिए बेहतर है

**Q: Quoting में क्या फर्क है?**
- Double quotes: Variables expand होते हैं
- Single quotes: Literal strings
- No quotes: Word splitting होता है

**Q: Error handling कैसे करते हो?**
- `set -e` = कोई error हो तो exit करो
- `set -o pipefail` = pipe में कोई fail हो तो exit
- `$?` = last command का exit status

---

## ✅ Checklist

- [ ] Bash syntax समझ गए
- [ ] Variables और data types
- [ ] Conditionals (if/else)
- [ ] Loops (for/while/until)
- [ ] Functions बना सकते हो
- [ ] Arrays handle कर सकते हो
- [ ] String manipulation
- [ ] File operations
- [ ] Text processing tools (grep, sed, awk)
- [ ] Error handling
- [ ] 20+ scripts लिख सकते हो
- [ ] Production scripts बना सकते हो

अगला: **Phase 10: Security & Hardening**
