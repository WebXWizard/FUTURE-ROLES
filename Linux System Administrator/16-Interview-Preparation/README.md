# Phase 16: Interview Preparation (15 Days)

> Master 200+ interview questions covering technical and behavioral aspects. Use production examples from your learning projects.

**Phase Duration**: 15 days  
**Interview Questions**: 200+

---

## 📋 Categories

```
1. FUNDAMENTALS (30 Q)
   - Linux basics, history, architecture
   - File systems, permissions, users
   
2. COMMANDS & TOOLS (40 Q)
   - File management, navigation
   - Process management, system commands
   - Text processing, scripting
   
3. USER & GROUP MANAGEMENT (20 Q)
   - Users, groups, permissions
   - sudo, SSH keys, security
   
4. NETWORKING (30 Q)
   - OSI Model, TCP/IP
   - Network commands, DNS, DHCP
   - Firewall, security
   
5. STORAGE & LVM (20 Q)
   - Partitions, file systems
   - LVM, RAID, backup
   
6. PROCESS & SERVICES (25 Q)
   - Process management
   - systemd, services
   - Signals, priorities
   
7. SCRIPTING & AUTOMATION (25 Q)
   - Bash scripting
   - Ansible, automation
   - Error handling
   
8. SECURITY (20 Q)
   - SSH hardening, firewall
   - Permissions, ACLs
   - SELinux, Fail2Ban
   
9. MONITORING & TROUBLESHOOTING (20 Q)
   - Monitoring tools
   - Log analysis
   - Performance tuning
   
10. REAL-WORLD SCENARIOS (25 Q)
    - Incident response
    - Production issues
    - Decision-making
    
11. BEHAVIORAL (20 Q)
    - Team work, communication
    - Conflict resolution
    - Learning mindset
```

---

## 💡 Sample Questions

### **Fundamentals**

**Q: What is the full form of Linux?**
A: Linux is just the kernel name. GNU/Linux is the complete operating system.

**Q: Boot process को explain करो**
A: 
1. BIOS/UEFI: Hardware initialize करता है
2. Bootloader (GRUB): Kernel को load करता है
3. Kernel: Main system software
4. Init system (systemd): Services start करता है
5. Login manager: User login

**Q: /proc filesystem - what is it?**
A: Virtual filesystem that shows information about current processes. It exists in memory, not on disk.

---

### **Commands**

**Q: 1 week पहले की सभी .log files को find करो?**
A: `find / -name "*.log" -mtime +7`

**Q: 100MB से बड़ी सभी files?**
A: `find / -type f -size +100M`

**Q: Specific user की सभी processes kill करो?**
A: `pkill -u username`

---

### **Networking**

**Q: What is OSI Model Layer 3?**
A: Network Layer - IP routing

**Q: What is the difference between TCP and UDP?**
A:
- TCP: Reliable, ordered, slower (connection-oriented)
- UDP: Fast, unreliable, no connection

**Q: DNS query कैसे काम करता है?**
A: Recursive resolution: Client → Resolver → Root NS → TLD NS → Authoritative NS

---

### **Real-World Scenarios**

**Q: A service suddenly failed in production - what would you do?**
A:
1. Immediately check service status: `systemctl status`
2. Check logs: `journalctl -u service -n 50`
3. Check dependencies: system resources, network, other services
4. Restart: `systemctl restart`
5. Verify: is the service running?
6. Monitor: watch for the next 1 hour
7. If still failing: escalate to team lead
8. Do root cause analysis

**Q: Disk suddenly became full - what would you do?**
A:
1. Check: `df -h`
2. Find large files: `du -sh /*`
3. Check logs: `du -sh /var/log/*`
4. Options:
   - Delete old logs/backups
   - Extend LVM volume
   - Move data to another disk
5. Implement solution
6. Monitor and verify

**Q: Server is slow - what would you do?**
A:
1. Check CPU: `top` - which process is using it?
2. Check Memory: `free -h` - how much available?
3. Check Disk I/O: `iostat`
4. Check Network: `netstat`
5. Identify bottleneck
6. Either: optimize code, add resources, or kill bad processes

---

### **Behavioral**

**Q: If you don't know a command, what would you do?**
A:
- `man command` - read the manual
- `--help` - check help option
- Google/Stack Overflow
- Ask a senior colleague
- Show a learning mindset

**Q: If your mistake caused an issue in production?**
A:
- Immediately tell your manager
- Focus on fixing the issue quickly
- Don't play the blame game
- In post-mortem: explain what you learned
- Suggest process improvements

---

## 📚 Interview Strategy

### **Before Interview**

```
1. Research करो
   - Company का tech stack
   - Systems उनके पास हैं
   - Recent projects
   
2. Prepare करो
   - 5-10 अच्छे से तैयार किए गए projects
   - Production में की गई troubleshooting के 3-5 examples
   - Linux fundamentals के concepts
   
3. Dress code
   - Professional attire
   - Clean और well-groomed
```

### **During Interview**

```
1. Communication
   - Clear और concise रहो
   - Unnecessary technical jargon avoid करो
   - "I don't know but I'll find out" - बेहतर है गलत जवाब देने से
   
2. Problem-solving
   - सवाल ध्यान से समझो
   - Systematic approach दिखाओ
   - Edge cases think करो
   
3. Culture fit
   - Honest रहो
   - Team player बनो
   - Learning mindset दिखाओ
```

### **After Interview**

```
1. Thank you email भेजो
2. Interview के 24 hours में follow-up
3. Feedback मांगो अगर rejected हो
4. Weak areas पर work करो
```

---

## ✅ Checklist: Interview Ready हो?

- [ ] 200+ questions के answers तैयार हो
- [ ] 5+ production projects में involved था
- [ ] Troubleshooting stories तैयार हो
- [ ] Technical concepts solid हैं
- [ ] Communication clear है
- [ ] Linux commands quick याद हैं
- [ ] Bash scripting demo ready है
- [ ] Professional का attitude है

---

अगला: **Phase 17: Portfolio Projects**
