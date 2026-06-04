# Phase 08: Process Management (8 Days)

> Learn how to monitor and control processes, check CPU and memory usage, and manage system resources effectively.

**Phase Duration**: 8 days

---

## 📋 What You'll Learn

```
├── Process Basics (PID, PPID)
├── Process Monitoring (ps, top, htop)
├── CPU & Memory Usage
├── Process Signals (SIGTERM, SIGKILL)
├── Process Priority (nice, renice)
├── Process States
├── Background & Foreground Jobs
├── Zombie Processes
└── Performance Monitoring
```

---

## 🗓️ Day-by-Day

### **DAY 1-2: Process Commands**

```bash
# Process listing:
ps aux                          # All processes
ps -ef                          # Full info
ps -ef --forest                 # Tree format
ps -u username                  # Specific user

# Real-time monitoring:
top                             # Real-time usage
htop                            # Better top (install if needed)

# Specific process:
ps -p 1234                      # Process 1234
pgrep firefox                   # Find by name
pidof apache2                   # Get PID
```

---

### **DAY 3-4: Process Signals**

```bash
# Signals (IPC - Inter Process Communication):
SIGTERM (15) - Graceful shutdown
SIGKILL (9)  - Forced kill (can't be ignored)
SIGSTOP (19) - Pause
SIGCONT (18) - Resume
SIGHUP (1)   - Hangup
SIGINT (2)   - Ctrl+C

# Sending signals:
kill -TERM 1234                 # Graceful
kill -9 1234                    # Force kill
kill -STOP 1234                 # Pause
kill -CONT 1234                 # Resume
killall firefox                 # Kill by name
```

---

### **DAY 5-6: Priority और Resource Control**

```bash
# Priority (nice value: -20 to +19):
nice -n 10 ./program            # Start with lower priority
renice -n 5 -p 1234             # Change running process

# Resource limits:
ulimit -a                       # Show all limits
ulimit -n 4096                  # Max open files
ulimit -u 256                   # Max processes
```

---

### **DAY 7-8: Monitoring & Troubleshooting**

```bash
# CPU usage:
top -b -n 1 | grep "Cpu(s)"
mpstat -P ALL 1 5               # Detailed CPU
sar 1 5                         # System Activity Report

# Memory:
free -h                         # Summary
cat /proc/meminfo               # Detailed
vmstat 1 5                       # Virtual memory

# I/O:
iostat 1 5
iotop                           # I/O per process

# Common issues:
"Process hung"     → send SIGTERM, then SIGKILL
"High CPU usage"   → top से find करो, then kill या optimize करो
"Memory leak"      → memory continuously बढ़ रहा है
"Zombie process"   → Parent process को restart करो
```

---

## 💡 Interview Questions

**Q: SIGTERM vs SIGKILL?**
- SIGTERM: Graceful, process cleanup कर सकता है
- SIGKILL: Forced, कोई cleanup नहीं

**Q: Process state क्या-क्या होते हैं?**
- Running (R), Sleeping (S), Disk sleep (D), Stopped (T), Zombie (Z)

**Q: Nice value क्या है?**
- -20 to +19: Lower value = higher priority
- Default = 0

---

## ✅ Checklist

- [ ] ps command से processes list कर सकते हो
- [ ] top/htop से monitoring कर सकते हो
- [ ] Signals को समझ गए
- [ ] Process को kill कर सकते हो gracefully
- [ ] Priority को manage कर सकते हो
- [ ] CPU/Memory usage analyze कर सकते हो
- [ ] Zombie processes को handle कर सकते हो

अगला: **Phase 09: Shell Scripting**
