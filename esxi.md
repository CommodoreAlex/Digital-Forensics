### **Virtual Machine ESXi Memory Forensics from a Snapshot**

---

## Video Demonstrations:
- [What is VMware?](https://www.youtube.com/watch?v=zPNCp9AV-vA)
- [VMware vCenter Server vs VMware ESXi: What's the Difference?](https://www.youtube.com/watch?v=xArL-GzFVOQ)
- [VMware Memory Forensics ](https://www.youtube.com/watch?v=P0yw93GJsYU)
- [i bought a new SERVER!! (VMware ESXi Setup and Install)](https://www.youtube.com/watch?v=apC1bOLbzbY)

### **Prerequisites**

1. **VMware ESXi Host**: Ensure that you have access to the VMware ESXi host where the virtual machine (VM) is running.
2. **Snapshot of the Virtual Machine**: You need to have a snapshot of the VM that you want to analyze.
3. **Forensic Tools**: You should have tools like **Volatility** or **Rekall** for memory analysis.
4. **Access to ESXi Datastore**: You need proper access rights to the datastore where the VM's snapshot and memory files are stored.
5. **Linux System**: For performing the forensic analysis, a Linux system (preferably Ubuntu or Kali) with forensic tools installed is required.

---

### **Step 1: Take a Snapshot of the Virtual Machine**

To analyze memory from a running VM, you must first take a snapshot to preserve the VM's memory state.

#### **Take Snapshot in VMware ESXi**

1. **Log in to VMware vSphere Client**.
2. **Select the VM**: Navigate to the VM you wish to analyze.
3. **Take Snapshot**:
    - Right-click on the VM and select **Snapshot > Take Snapshot**.
    - Provide a name and description for the snapshot.
    - Select the option to **Snapshot the Virtual Machine's memory** to capture the state of the VM's RAM.
4. **Confirm**: Once the snapshot is taken, it will include a memory dump of the virtual machine.

---

### **Step 2: Access the Virtual Machine's Snapshot Files**

1. **Locate the VM Files**:

Log in to the **VMware ESXi host** through SSH (using an account with sufficient privileges).

Navigate to the datastore directory where the VM’s files are stored, typically found under `/vmfs/volumes/`:
```bash
cd /vmfs/volumes/datastore1/VMName/
```
    
2. **Find the Memory Dump**:
    - The snapshot will generate a file with a `.vmsn` extension (for snapshot data) and a `.vmem` file (for memory dump).
    - The **`.vmem`** file is what you’ll use for memory forensics.

```bash
ls -l
```

You should see files like:
- `VMName.vmsn` (snapshot descriptor)
- `VMName.vmem` (virtual machine memory dump)

---

### **Step 3: Transfer the Memory Dump to Your Analysis System**

1. **Copy the Memory Dump**:
    - Use `scp` (secure copy) or another secure file transfer method to copy the `.vmem` file to your analysis system (Linux system).
```bash
scp user@esxihost:/vmfs/volumes/datastore1/VMName/VMName.vmem /path/to/analysis/machine/
```

2. **Verify the Transfer**:
    - After the transfer completes, ensure that the file is intact and has been copied correctly.

---

### **Step 4: Analyze the Memory Dump Using Volatility**

Now that you have the memory dump file, you can analyze it using **Volatility 3**, a memory forensics tool.

#### **Install Volatility 3 (if not already installed)**

If Volatility 3 isn’t installed on your Linux system, you can install it as follows:

1. Install the dependencies:
```bash
sudo apt update
sudo apt install -y git python3-pip
sudo apt install -y libafflib0 python3-dev libdwarf-dev build-essential
```

2. Clone the Volatility 3 repository:
```bash
git clone https://github.com/volatilityfoundation/volatility3.git
cd volatility3
```

3. Install Volatility 3 using pip:
```bash
pip3 install -r requirements.txt
```

---

### **Step 5: Run Volatility to Analyze the Memory Dump**

Now, let's use Volatility 3 to analyze the `.vmem` file. You will need to specify the memory profile based on the virtual machine's operating system.

#### **List Available Profiles (OS Types)**

To list available profiles that Volatility supports, you can use:
```bash
vol.py -h
```

#### **Run Volatility Analysis**

1. **Determine the Profile**:
    - The VM image you’ve captured may run Windows, Linux, or another operating system. You will need to identify the correct profile for your memory image. For example, if it’s a Windows 10 image, you would use a profile like `Win10x64` or similar.
2. **Run Volatility for Analysis**:
    - You can run a basic command to analyze the `.vmem` file. For example, to display basic information about the memory dump:

```bash
python3 vol.py -f VMName.vmem windows.info
```

Replace `windows.info` with the appropriate plugin based on the operating system. For Linux memory, you might use `linux.pslist` or other Linux-specific plugins:
```bash
python3 vol.py -f VMName.vmem linux.pslist
```


#### **Common Volatility Plugins for Memory Analysis:**

- **`windows.info`**: Provides basic information about the memory dump.
- **`windows.pslist`**: Lists running processes in the snapshot.
- **`windows.dlllist`**: Lists loaded DLLs in the system.
- **`linux.pslist`**: Lists running processes for Linux.
- **`linux.netstat`**: Displays network connections.

For example, to see the processes running in the virtual machine:
```bash
python3 vol.py -f VMName.vmem windows.pslist
```

---

### **Step 6: Investigate and Extract Artifacts**

You can use other Volatility plugins to extract additional forensic artifacts such as:

**Command History**: Extract command history from shell or terminal processes.
```bash
python3 vol.py -f VMName.vmem linux.bash
```

**Network Connections**: Find active or closed network connections.
```bash
python3 vol.py -f VMName.vmem linux.netstat
```

**Running Processes**: Get a list of running processes during the snapshot.
```bash
python3 vol.py -f VMName.vmem linux.pslist
```

---

### **Step 7: Interpret the Results**

After performing the analysis, carefully review the output to uncover valuable information about the virtual machine's state at the time the snapshot was taken. Key artifacts might include:

- **Running processes**: Identify malicious or suspicious processes.
- **Network connections**: Examine established connections that may indicate exfiltration or malicious communication.
- **File system data**: Extract information about files loaded into memory, which may indicate tampering or malicious activity.

---

### **Conclusion**

Performing **memory forensics** from a **VMware ESXi snapshot** is a powerful method for investigating incidents and gaining insights into a virtual machine's state at the time of an event. With tools like **Volatility 3**, you can efficiently analyze memory dumps for forensic evidence. By following this guide, you can extract valuable data to support investigations and provide evidence for potential security incidents.
