### **TShark Tutorial: Command-Line Network Analysis**

---

### **Prerequisites**

1. **TShark Installation**: Ensure that TShark is installed on your Linux or Windows system.
2. **Network Interface**: You should know the network interface you will be using to capture packets (e.g., `eth0`, `wlan0`, etc.).
3. **Permissions**: You may need administrator or root permissions to capture network packets.

---

### **Step 1: Install TShark**

#### **For Linux (Ubuntu/Debian-based distributions)**

1. **Update the package list**:
```bash
sudo apt update
```

2. **Install TShark**:
```bash
sudo apt install tshark
```

3. **Grant Non-Root Access to TShark** (optional but recommended):
```bash
sudo usermod -aG wireshark $(whoami)
```

During installation, you might be prompted to allow non-superusers to capture packets. If not, add your user to the `wireshark` group:

Log out and log back in to apply the group changes.

4. **Verify Installation**:
```bash
tshark -v
```

You should see TShark version information if it's installed correctly.
#### **For Windows**

1. Download the TShark installer from the Wireshark download page.
2. Run the installer and follow the instructions to install TShark.

---

### **Step 2: Start Capturing Network Traffic with TShark**

To begin capturing packets with TShark, you'll need to specify the network interface and other options.

1. **List Available Network Interfaces**: To see a list of available network interfaces for packet capture:
```bash
tshark -D
```


This command will display all the interfaces available on your system (e.g., `eth0`, `wlan0`).

2. **Start Capturing Traffic**: Once you know the interface, you can start capturing packets. Replace `1` with the number of your desired network interface (e.g., `eth0` or `wlan0`).
```bash
sudo tshark -i 1
```

This will capture all packets on the selected interface. You can stop the capture by pressing `Ctrl + C`.


---

### **Step 3: Apply Filters in TShark**

Filters are used to focus on specific types of traffic during the capture process. Here are some examples:

#### **Capture Filters**:

Capture filters are applied before the capture process starts and can limit which packets are captured.

1. **Capture Only TCP Traffic**:
```bash
sudo tshark -i 1 -f "tcp"
```

2. **Capture Traffic on a Specific Port (e.g., Port 80)**:
```bash
sudo tshark -i 1 -f "tcp port 80"
```

3. **Capture Traffic from a Specific IP Address**:
```bash
sudo tshark -i 1 -f "host 192.168.1.100"
```


#### **Display Filters**:

Display filters are applied after packets are captured and are useful for narrowing down results.

1. **Display Only HTTP Traffic**:
```bash
sudo tshark -i 1 -Y "http"
```

2. **Display Packets with a Specific Source IP**:
```bash
sudo tshark -i 1 -Y "ip.src == 192.168.1.100"
```

3. **Display Packets from a Specific TCP Port**:
```bash
sudo tshark -i 1 -Y "tcp.port == 80"
```

4. **Display Only TCP Traffic with a Specific Flag Set**:
```bash
sudo tshark -i 1 -Y "tcp.flags.syn == 1 and tcp.flags.ack == 1"
```

---

### **Step 4: Saving and Exporting Captures**

You can save the captured packets in various formats for later analysis.

1. **Save to a File**: To save the captured packets to a file, use the `-w` option. For example, save to `capture.pcap`:
```bash
sudo tshark -i 1 -w capture.pcap
```

2. **Save with a Timestamp**: If you want to save the file with a timestamp, you can include it in the filename:
```bash
sudo tshark -i 1 -w capture_$(date +%Y%m%d_%H%M%S).pcap
```

3. **Convert Captured Packets to a Different Format**: To convert the saved `.pcap` file to another format (e.g., CSV):
```bash
tshark -r capture.pcap -T fields -e frame.number -e ip.src -e ip.dst -e tcp.port -E header=y -E separator=, > capture.csv
```


---

### **Step 5: Analyzing the Capture**

After capturing and saving network traffic, you can analyze the capture in multiple ways.

1. **Read a Capture File**: Use the `-r` option to read and analyze a saved capture file.
```bash
tshark -r capture.pcap
```

2. **Display Specific Fields**: You can display specific fields from the capture file. For example, to display source and destination IP addresses, and the protocol:
```bash
tshark -r capture.pcap -T fields -e ip.src -e ip.dst -e ip.proto
```

3. **Export Selected Data**: You can export certain packet details, such as IP addresses and protocols, to CSV or other formats.
```bash
tshark -r capture.pcap -T fields -e ip.src -e ip.dst -e tcp.port -E header=y -E separator=, > export.csv
```

4. **Summarize the Capture**: Use the `-z` option to get a summary of the capture, such as packet counts, protocol distribution, and more.
```bash
tshark -r capture.pcap -z io,stat,0
```


---

### **Step 6: TShark Statistics**

TShark offers a number of useful statistics for analyzing the traffic in a capture.

1. **Protocol Hierarchy**: To view the distribution of protocols in the capture:
```bash
tshark -r capture.pcap -z protos
```

2. **Packet Count per Host**: To view how many packets were sent from each IP address:
```bash
tshark -r capture.pcap -z conv,ip
```

3. **IO Graphs**: Generate IO graphs to visualize network traffic patterns over time:
```bash
tshark -r capture.pcap -z io,stat,0
```


---

### **Step 7: Use TShark in Scripts**

TShark is well-suited for automation and can be easily integrated into shell scripts or other automation tools.

For example, to capture packets for a specific duration and save them to a file:
```bash
#!/bin/bash
# Capture packets for 60 seconds
tshark -i 1 -w capture_$(date +%Y%m%d_%H%M%S).pcap -a duration:60
```

---

### **Step 8: TShark Command Examples**

Here are a few common use cases for TShark:

1. **Capture and Save Traffic to a File**:
```bash
sudo tshark -i eth0 -w traffic.pcap
```

2. **Capture HTTP Traffic Only**:
```bash
sudo tshark -i eth0 -Y "http"
```

3. **Display Packets for a Specific IP Address**:
```bash
tshark -r capture.pcap -Y "ip.addr == 192.168.1.100"
```

4. **Capture Traffic for 60 Seconds**:
```bash
sudo tshark -i eth0 -a duration:60 -w capture.pcap
```

5. **Show TCP Conversation Summary**:
```bash
tshark -r capture.pcap -z conv,tcp
```


---

### **Conclusion**

TShark is a powerful tool for network analysis and troubleshooting, especially in environments where you need to work from the command line or automate network packet captures. It provides similar functionality to Wireshark but without the GUI, making it ideal for remote or script-based analysis.

By using this tutorial, you should now be able to use TShark for capturing, filtering, and analyzing network traffic, whether on a local machine or in an automated process.
