# Linux Forensics and EXT File System Analysis

## 1. **Introduction to Linux Forensics**
Linux forensics is crucial for investigating security incidents, analyzing system behavior, and recovering lost or deleted files. Unlike NTFS in Windows, Linux primarily uses **EXT (Ext2, Ext3, Ext4)**, **XFS**, and **Btrfs** as file systems. Understanding how these file systems store and manage data is key to forensic investigations.

---

## Video Demonstrations:
- [The Linux File System in 4 Minutes | A MUST Learn](https://www.youtube.com/watch?v=995-SYn6960)
- [The Linux Kernel: What it is, and how it works!](https://www.youtube.com/watch?v=JDfo2Lc7iLU)
- [Pentester Academy Linux Forensics course Filesystem analysis part1 Ext filesystem basics](https://www.youtube.com/watch?v=gNxSCHecByI)
- [Linux Forensics Tutorial || Linux file system forensics](https://www.youtube.com/watch?v=HTEj8UY2TA8&t=4175s)
- [Linux Forensics with Linux - CTF Walkthrough](https://www.youtube.com/watch?v=bjHh6Tz72gA)

---

## 2. **Key Components of Linux Forensics**
When analyzing a Linux system, forensic investigators focus on several key areas:

### **A. File System Structure and EXT Journaling**
1. **Superblock**
   - Stores metadata about the file system, such as size, block count, and status.
   - Can be examined with:
     ```
     sudo dumpe2fs /dev/sdX | grep -i superblock
     ```
   - Corrupted superblocks can sometimes be restored using backup copies.

2. **Inodes**
   - Each file and directory has an inode storing:
     - File size, owner, group, and permissions
     - Timestamps (creation, modification, access, deletion)
     - Data block locations
   - View inode details:
     ```
     stat /path/to/file
     ls -i /path/to/file
     ```

3. **EXT Journal ($LogJournal in Ext3/Ext4)**
   - Records file system changes before they are committed.
   - Useful for recovering deleted or modified files.
   - Extract journal data:
     ```
     sudo debugfs /dev/sdX
     journal dump
     ```

### **B. Linux Timestamps and Time Analysis**
Linux maintains multiple timestamps, critical for forensic investigations:
- **atime (Access Time):** Last time the file was read.
- **mtime (Modified Time):** Last time the file content was modified.
- **ctime (Change Time):** Last time file metadata was changed.
- **crtime (Creation Time, Ext4 only):** Original file creation timestamp.

Check timestamps with:
```bash
stat filename
```

### **C. Deleted File Recovery**
- In EXT-based file systems, deleting a file removes its inode reference but often leaves data intact until overwritten.
- **Recovery Tools:**
  - `extundelete` – Recovers deleted files on Ext3/Ext4.
  - `photorec` – Recovers files based on signatures (useful for all file systems).
  - `testdisk` – Recovers lost partitions and files.

Example recovery command:
```bash
sudo extundelete /dev/sdX --restore-all
```

### **D. Log Files and System Artifacts**
Linux logs are stored under `/var/log/`, containing valuable forensic evidence:
- **/var/log/auth.log** – User authentication logs.
- **/var/log/syslog** – General system logs.
- **/var/log/kern.log** – Kernel activity logs.
- **/var/log/wtmp & /var/log/btmp** – Login/logout history (view with `last` and `lastb`).

Example:
```bash
cat /var/log/auth.log | grep 'Failed password'
```

### **E. Process and Memory Forensics**
1. **Live Process Analysis**
   - List running processes:
     ```bash
     ps aux
     ```
   - Identify suspicious processes:
     ```bash
     lsof -i -n -P
     ```
   - Check open network connections:
     ```bash
     netstat -tulnp
     ```

2. **Memory Dump Analysis**
   - Capture memory dump:
     ```bash
     sudo dd if=/dev/mem of=/root/memdump.raw bs=1M
     ```
   - Analyze with **Volatility**:
     ```bash
     volatility -f memdump.raw --profile=Linux pslist
     ```

### **F. User Activity and Artifacts**
- **Bash History:** `~/.bash_history`
- **Cron Jobs:** `/etc/crontab` & `/var/spool/cron/`
- **SSH Keys and Logins:** `~/.ssh/authorized_keys` & `/var/log/secure`
- **SUID and SGID Binaries (Privilege Escalation Risks):**
  ```bash
  find / -perm -4000 -type f 2>/dev/null
  ```

---

## 3. **Forensic Tools for Linux Analysis**
Here are some essential tools for Linux forensic investigations:

| Tool | Description |
|------|-------------|
| **Autopsy** | Open-source forensic platform |
| **Sleuth Kit** | CLI forensic toolkit for file system analysis |
| **Volatility** | Memory forensics framework |
| **TestDisk** | Recovers lost partitions and files |
| **Extundelete** | Recovers deleted files on Ext3/Ext4 |
| **chkrootkit & rkhunter** | Detects rootkits and malware |
| **Wireshark** | Network traffic analysis |
| **Foremost** | File carving tool for data recovery |
| **Log2timeline (Plaso)** | Creates forensic timelines |

---

## 4. **Conclusion**
Understanding Linux forensics and EXT file system artifacts is critical for incident response and digital investigations. Key forensic areas include analyzing timestamps, recovering deleted data, investigating system logs, and extracting memory dumps. By leveraging forensic tools, investigators can reconstruct system events, detect anomalies, and recover crucial evidence.

🔍 **Challenge:** Try recovering a deleted file using `extundelete` or create a forensic timeline with Plaso!

---

### **Further Reading & Resources**
- [Linux Forensics by Lenny Zeltser](https://zeltser.com/linux-forensics/)
- [Sleuth Kit & Autopsy](https://www.sleuthkit.org/)
- [Volatility Framework](https://www.volatilityfoundation.org/)
- [Linux Journal Analysis](https://linuxconfig.org/analyzing-linux-system-log-files)

