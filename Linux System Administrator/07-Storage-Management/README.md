# Phase 07: Storage Management (12 Days)

> Learn how to organize disks, understand LVM, RAID, and backups. The most critical skill for production systems.

**Phase Duration**: 12 days  
**Prerequisites**: Complete Phase 1-6

---

## 📋 What You'll Learn

```
├── Disk Partition (fdisk, parted)
├── File Systems (ext4, XFS, Btrfs)
├── LVM (Logical Volume Manager)
├── RAID (Redundant Array of Independent Disks)
├── Mount/Unmount
├── Disk Usage Analysis
├── Swap Management
├── Backup Strategies
├── Snapshots
└── Disaster Recovery
```

---

## 🗓️ संक्षिप्त दिन-दर-दिन

### **DAY 1-2: Partitioning और File Systems**

```bash
# Disk देखना:
lsblk                          # Block devices tree
fdisk -l                       # Detailed disk info
parted -l                      # Partitions

# Partition बनाना:
sudo fdisk /dev/sda            # Interactive mode
sudo parted /dev/sda mkpart primary ext4 1MiB 10GB  # Direct

# File system बनाना:
sudo mkfs.ext4 /dev/sda1       # ext4
sudo mkfs.xfs /dev/sda1        # XFS
sudo mkfs.btrfs /dev/sda1      # Btrfs

# Mount करना:
sudo mkdir /mnt/data
sudo mount /dev/sda1 /mnt/data
sudo umount /mnt/data
```

---

### **DAY 3-4: LVM - Logical Volume Manager**

```bash
# LVM की hierarchy:
# Physical Volume (PV) - actual disk
#   ↓
# Volume Group (VG) - collection of PVs
#   ↓
# Logical Volume (LV) - like partition, but flexible

# Create LVM:
sudo pvcreate /dev/sda1 /dev/sda2      # Physical volumes
sudo vgcreate myvg /dev/sda1 /dev/sda2 # Volume group
sudo lvcreate -n mylv -L 10G myvg      # Logical volume

# Format और mount:
sudo mkfs.ext4 /dev/myvg/mylv
sudo mount /dev/myvg/mylv /mnt/data

# Expand LVM (key advantage!):
sudo lvextend -L +5G /dev/myvg/mylv    # Expand LV
sudo resize2fs /dev/myvg/mylv          # Resize file system
```

---

### **DAY 5-7: RAID - Redundancy**

```bash
# RAID levels:
RAID 0: Striping (fast, no redundancy) - 2+ disks
RAID 1: Mirroring (redundancy) - 2 disks
RAID 5: Striping with parity (balance) - 3+ disks
RAID 6: Dual parity (safer) - 4+ disks
RAID 10: Mirrored stripes (speed + safety) - 4+ disks

# Create RAID:
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 \
  /dev/sda1 /dev/sdb1

# Check status:
sudo cat /proc/mdstat
sudo mdadm --detail /dev/md0
```

---

### **DAY 8-9: Disk Usage and Quotas**

```bash
# Disk usage analysis:
df -h                          # Partition usage
du -sh /path/*                 # Directory size
ncdu /path                     # Interactive disk analyzer
iostat -x 1                    # I/O statistics

# Quotas (limit disk usage):
sudo edquota -u username       # Edit user quota
sudo setquota -u username 0 1000000 0 100000 /
```

---

### **DAY 10-11: Swap और Performance**

```bash
# Swap देखना:
swapon -s                      # Active swaps
free -h                        # Memory + swap

# Swap file बनाना:
sudo dd if=/dev/zero of=/swapfile bs=1G count=4
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# Performance tuning:
swappiness set करना (default 60):
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

---

### **DAY 12: Practical Scenarios**

```bash
# Scenario 1: Disk भर गया - क्या करें?
1. Largest files find करो: find / -type f -size +100M
2. Logs rotate करो: logrotate
3. Temp files clean करो: rm /tmp/*
4. Or: Extend LVM volume

# Scenario 2: RAID disk fail हो गई
1. Status check: sudo mdadm --detail /dev/md0
2. Failed disk remove: sudo mdadm /dev/md0 -f /dev/sda1
3. New disk add: sudo mdadm /dev/md0 -a /dev/sdc1
4. Rebuild होगी automatically

# Scenario 3: Performance slow है
1. iostat से check करो
2. Slow disks identify करो
3. RAID optimize करो
4. Cache enable करो
```

---

## 💡 Interview Questions

**Q: LVM क्यों use करते हो fdisk के जगह?**
- Flexibility - size change कर सकते हो reboot के बिना
- Snapshots ले सकते हो
- Multiple disks को एक pool में combine कर सकते हो

**Q: RAID 5 vs RAID 10 - कौन बेहतर?**
- RAID 5: Cost-effective, कम disk
- RAID 10: Faster, better redundancy, expensive

**Q: LVM expand करते समय क्या गलती होती है?**
- lvextend करने के बाद resize2fs/xfs_growfs करना भूल जाते हैं
- फिर भी LV expand हो जाता है पर file system नहीं

**Q: Swap कितना होना चाहिए?**
- RAM ≤ 2GB: 2x RAM
- RAM > 2GB: RAM के बराबर या 0 (SSD के लिए)

---

## ✅ Checklist

- [ ] Partitions create कर सकते हो
- [ ] File systems understand करते हो
- [ ] LVM को समझ गए और use कर सकते हो
- [ ] RAID concepts समझ गए
- [ ] Disk usage analyze कर सकते हो
- [ ] LVM expand कर सकते हो
- [ ] RAID troubleshoot कर सकते हो
- [ ] Swap configure कर सकते हो

अगला: **Phase 08: Process Management**
