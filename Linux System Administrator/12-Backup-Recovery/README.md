# Phase 12: Backup & Disaster Recovery (8 Days)

> Data loss is the biggest disaster in production. Learn backup strategies, recovery plans, and tools like rsync and tar.

**Phase Duration**: 8 days

---

## 📋 What You'll Learn

```
├── Backup Strategies (Full, Incremental, Differential)
├── Backup Tools (tar, rsync, bacula)
├── Remote Backup
├── Disaster Recovery Planning
├── Recovery Testing
├── Retention Policies
├── Compression
├── Encryption
├── Automation
└── Real-world Scenarios
```

---

## 🗓️ गाइड

### **DAY 1-2: Backup Tools**

```bash
# tar - Archive करना:
tar -cvzf backup_$(date +%Y%m%d).tar.gz /important/data
tar -xvzf backup.tar.gz                 # Restore

# rsync - Incremental backup:
rsync -avz --delete /source /destination
rsync -avz -e ssh /source remote:/backup

# Create backup script:
#!/bin/bash
BACKUP_DIR="/backups"
SOURCE="/data"
DATE=$(date +%Y%m%d)
tar -czf $BACKUP_DIR/backup_$DATE.tar.gz $SOURCE
# Keep only last 30 days
find $BACKUP_DIR -mtime +30 -delete
```

---

### **DAY 3-4: Remote Backup**

```bash
# SSH के साथ:
rsync -avz -e ssh /data user@server:/backups

# Automated script:
#!/bin/bash
REMOTE="user@backup-server"
ssh $REMOTE "mkdir -p /backups/$(date +%Y/%m)"
tar -czf - /important/data | \
    ssh $REMOTE "cat > /backups/$(date +%Y/%m/%d).tar.gz"
```

---

### **DAY 5-6: Disaster Recovery**

```bash
# Recovery Testing:
1. Full backup लो
2. Test environment में restore करो
3. Data verify करो
4. Document करो
5. Regular intervals पर repeat करो

# Bare-metal recovery:
# Live USB से boot करो
# Disk image restore करो
# Bootloader reinstall करो
```

---

### **DAY 7-8: Real Scenarios**

```bash
# Scenario 1: Database backup
#!/bin/bash
mysqldump -u root -p database_name | \
    gzip > /backups/db_$(date +%Y%m%d).sql.gz

# Scenario 2: Application backup
rsync -avz --delete /opt/app /backups/app_$(date +%Y%m%d)

# Scenario 3: Incremental backup strategy
FULL_DAY=0  # Sunday को full backup
DAY=$(date +%w)
if [ $DAY -eq $FULL_DAY ]; then
    tar -czf /backups/full_$(date +%Y%m%d).tar.gz /data
else
    find /data -mtime 0 -print0 | \
        tar --null -czf /backups/inc_$(date +%Y%m%d).tar.gz -T -
fi
```

---

## 💡 3-2-1 Rule

```
3 Copies: Original + 2 backups
2 Different Media: Local disk + Remote
1 Offsite: One copy outside facility

Example:
- Production system: 1 copy
- Local NAS: 1 copy
- Cloud backup: 1 copy
```

---

अगला: **Phase 13: Cloud Basics**
