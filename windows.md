# NTFS Forensics and Master File Table (MFT) Analysis

## 1. **Introduction to NTFS Forensics**
NTFS (New Technology File System) is the default file system for modern Windows operating systems. When conducting forensic investigations on NTFS systems, understanding how data is stored, modified, and deleted is crucial. One of the most valuable sources of forensic evidence in NTFS is the **Master File Table (MFT)**, which contains metadata for every file and directory on the system.

---

## Video Demonstrations:
- [FAT32 vs exFAT vs NTFS - Windows File Systems](https://www.youtube.com/watch?v=bYjQakUxeVY)
- [NTFS Forensics and the Master File Table](https://www.youtube.com/watch?v=xW5UwDztkX4)

---

## 2. **Key Components of NTFS Forensics**
When analyzing an NTFS filesystem, forensic investigators focus on several key areas:

### **A. Master File Table (MFT)**
- The **MFT** is a relational database storing information about every file and directory, including:
  - Filename
  - File size
  - Timestamps (creation, modification, access, entry modified)
  - File attributes
  - Parent directory
  - Location of data on disk (resident or non-resident)
- **Forensic Significance**:
  - Tracks deleted files that may still have recoverable metadata.
  - Helps identify time-based anomalies (e.g., timestamp manipulation).
  - Can reveal hidden or alternate data streams (ADS).

### **B. File System Journals and Logs**
1. **$LogFile**
   - NTFS transaction log that records file system changes before they are committed.
   - Useful for recovering deleted or overwritten data.
2. **$UsnJrnl (Update Sequence Number Journal)**
   - Records metadata changes for files, tracking modifications even after deletion.
   - Helps in identifying tampered or suspicious activity.
3. **$Secure**
   - Stores NTFS file permissions (ACLs), useful for tracking user access patterns.

### **C. Timestamps and Time Analysis**
NTFS maintains four key timestamps for every file:
- **$STANDARD_INFORMATION**
  - Creation Time (C)
  - Modified Time (M)
  - Access Time (A)
  - Entry Modified Time (E)
- **$FILENAME**
  - Contains another set of timestamps, which can help identify timestamp tampering.

Forensic tools like **Plaso (log2timeline)** and **MFT Parser** can help create a timeline of file activity.

### **D. Alternate Data Streams (ADS)**
- NTFS allows files to have hidden data streams using the `:` character.
- **Example:** A malicious executable hidden inside a text file:
  ```
  notepad.exe myfile.txt:malware.exe
  ```
- **Forensic Detection:** Use `dir /r` in Windows or `streams.exe` from Sysinternals to identify ADS files.

### **E. Deleted File Recovery**
- When a file is deleted, its MFT entry is marked as available but remains on disk until overwritten.
- Tools like **Autopsy**, **FTK Imager**, and **TestDisk** can recover deleted files by parsing MFT records.

### **F. Prefetch Files (Application Execution History)**
- Stored in `C:\Windows\Prefetch`
- Helps in identifying program execution times and paths.
- Useful for tracking malware execution or user activity.

### **G. Windows Registry Artifacts**
- **Recent File Access:** `NTUSER.DAT` and `USRCLASS.DAT`
- **Mounted Devices:** `SYSTEM\MountedDevices`
- **USB Forensics:** `SYSTEM\CurrentControlSet\Enum\USBSTOR`
- **Executed Programs:** `MUICache`, `AppCompatCache`, `UserAssist`

---

## 3. **Forensic Tools for NTFS Analysis**
Here are some essential tools for NTFS and MFT analysis:

| Tool | Description |
|------|-------------|
| **Autopsy** | Open-source digital forensics platform |
| **FTK Imager** | Acquires and analyzes disk images |
| **Sleuth Kit** | CLI forensic toolkit for NTFS analysis |
| **MFT Parser** | Extracts and analyzes MFT records |
| **Plaso (log2timeline)** | Creates forensic timelines |
| **Windows Event Viewer** | Analyzes event logs |
| **Sysinternals Suite** | Useful for system monitoring and forensic analysis |
| **Rekall & Volatility** | Memory forensics frameworks |

---

## 4. **Conclusion**
Understanding NTFS and its forensic artifacts is essential for investigating security incidents, cybercrime, and digital forensics cases. The MFT is one of the most valuable sources of forensic evidence, offering insights into file activity, deletions, timestamps, and hidden data streams. By leveraging forensic tools, investigators can reconstruct events, recover deleted data, and detect anomalies in Windows systems.

🔍 **Challenge:** Try analyzing an MFT dump using Autopsy or Sleuth Kit and extract deleted file records!

---

### **Further Reading & Resources**
- [Microsoft NTFS Documentation](https://docs.microsoft.com/en-us/windows-server/storage/ntfs/ntfs-overview)
- [Digital Forensics with Autopsy](https://www.sleuthkit.org/autopsy/)
- [Plaso - Timelining](https://github.com/log2timeline/plaso)
- [Alternate Data Streams Guide](https://www.fireeye.com/blog/threat-research/2013/08/know-your-enemy-hidden-threats.html)
