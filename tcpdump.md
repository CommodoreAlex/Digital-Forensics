### **TCPDump Guide: Network Traffic Capture and Analysis**

## What is TCPDUMP?
tcpdump is a powerful command-line packet analyzer used for network traffic capture and analysis. It allows users to intercept, filter, and inspect packets on a network interface in real-time. Commonly used by network administrators and security professionals, tcpdump helps with troubleshooting, monitoring, and forensic investigations.

Key Features:
- Captures live traffic from network interfaces (e.g., Ethernet, Wi-Fi).
- Filters packets using Berkeley Packet Filter (BPF) syntax.
- Can save packet captures to files (e.g., .pcap) for later analysis.

---

## Video Demonstrations
- [tcpdump - Traffic Capture & Analysis](https://www.youtube.com/watch?v=1lDfCRM6dWk)


### **Prerequisites**

1. **TCPDump Installation**: Ensure that TCPDump is installed on your system.
2. **Permissions**: You need to have root or superuser privileges to capture packets on most network interfaces.
3. **Network Interface**: You should know which network interface you want to capture packets from (e.g., `eth0`, `wlan0`, etc.).

---

### **Step 1: Install TCPDump**

#### **For Linux (Ubuntu/Debian-based distributions)**

1. **Update Package List**:
```bash
sudo apt update
```

2. **Install TCPDump**:
```bash
sudo apt install tcpdump
```

3. **Verify Installation**: After installation, you can verify TCPDump's version to ensure it's installed correctly:
```bash
tcpdump --version
```

#### **For Windows**

1. **Download and Install WinDump**: WinDump is the Windows version of TCPDump. Download it from WinDump's website.
2. **Install WinPcap or Npcap**: WinDump requires WinPcap or Npcap for capturing packets. Install one of these network drivers.

---

### **Step 2: List Network Interfaces**

Before you start capturing packets, you need to know which network interfaces are available on your system. To list all available interfaces:
```bash
sudo tcpdump -D
```

This command will show a list of interfaces on your system, like:
```bash
1. eth0
2. wlan0
3. lo
```

Choose the interface that corresponds to the network you want to monitor.

---

### **Step 3: Start Capturing Network Traffic**

To start capturing packets on a specific interface, use the following command:
```bash
sudo tcpdump -i <interface>
```

Replace `<interface>` with the name of the network interface (e.g., `eth0`, `wlan0`, etc.). For example:
```bash
sudo tcpdump -i eth0
````

This will start capturing all packets on the selected interface and print them to the terminal.

#### **Stop the Capture**:

You can stop the capture at any time by pressing `Ctrl + C`.

---

### **Step 4: Apply Filters for Capturing Packets**

TCPDump allows you to apply filters to capture specific types of traffic. Filters can be applied using the `-f` option, such as capturing only TCP traffic, packets from specific IP addresses, or traffic on specific ports.

#### **Capture Specific Traffic**:

1. **Capture Only TCP Traffic**:
```bash
sudo tcpdump -i eth0 tcp
```

2. **Capture Traffic from a Specific IP Address**:
```bash
sudo tcpdump -i eth0 host 192.168.1.100
```

3. **Capture Traffic from a Specific Port**: To capture HTTP traffic (port 80):
```bash
sudo tcpdump -i eth0 port 80
```

4. **Capture Traffic to/from a Specific IP Address**: To capture packets from or to `192.168.1.100`:
```bash
sudo tcpdump -i eth0 src or dst 192.168.1.100
```

5. **Capture Only UDP Traffic**:
```bash
sudo tcpdump -i eth0 udp
```

6. **Capture Traffic for a Specific Protocol**:
```bash
sudo tcpdump -i eth0 icmp
```

7. **Capture Traffic on a Specific Subnet**:
```bash
sudo tcpdump -i eth0 net 192.168.1.0/24
```


---

### **Step 5: Save Captured Packets to a File**

To save the captured packets to a file for later analysis, use the `-w` option. By default, TCPDump saves the packets in the **PCAP** format, which can later be opened in tools like Wireshark or TCPDump:
```bash
sudo tcpdump -i eth0 -w capture.pcap
```


This will capture packets on `eth0` and save them to the `capture.pcap` file.

---

### **Step 6: Read and Analyze Saved Capture Files**

To analyze a previously captured file, use the `-r` option:
```bash
sudo tcpdump -r capture.pcap
```

This will display the contents of the `capture.pcap` file.

---

### **Step 7: Displaying Packet Information**

By default, TCPDump provides a brief summary of each packet. You can control the verbosity with several options:

1. **Verbose Output**: The `-v` flag increases the verbosity, showing more details:
```bash
sudo tcpdump -i eth0 -v
```

2. **Even More Verbose Output**: Use the `-vv` or `-vvv` flags to get more detailed packet information.
```bash
sudo tcpdump -i eth0 -vvv
```

3. **Show Link-Level Information**: The `-e` option shows link-level (Ethernet) information such as MAC addresses:
```bash
sudo tcpdump -i eth0 -e
```

4. **Display Packet Timestamps**: The `-tt` option shows precise timestamps for each packet.
```bash
sudo tcpdump -i eth0 -tt
```


---

### **Step 8: Capturing and Displaying Specific Packet Information**

You can also capture specific fields from each packet, such as IP addresses, protocols, or flags.

1. **Display Source and Destination IP Address**:
```bash
sudo tcpdump -i eth0 -n -tttt -v
```

2. **Display TCP Handshake Information**: Capture only SYN, SYN-ACK, and ACK flags (useful for analyzing TCP handshakes):
```bash
sudo tcpdump -i eth0 'tcp[tcpflags] & (tcp-syn|tcp-ack) != 0'
```

---

### **Step 9: Apply More Complex Filters**

TCPDump filters can get complex, using combinations of conditions. Filters are applied using logical operators like `and`, `or`, and `not`.

1. **Capture Traffic to/from a Specific IP and Specific Port**:
```bash
sudo tcpdump -i eth0 host 192.168.1.100 and port 80
```

2. **Capture UDP Traffic and Ignore ICMP**:
```bash
sudo tcpdump -i eth0 udp and not icmp
```

3. **Capture Traffic from a Subnet and Exclude Specific Host**:
```bash
sudo tcpdump -i eth0 net 192.168.1.0/24 and not host 192.168.1.100
```


---

### **Step 10: Capture Traffic for a Specific Duration**

You can limit the capture time by specifying the number of packets to capture or the duration:

1. **Capture a Specific Number of Packets**:
```bash
sudo tcpdump -i eth0 -c 100
```

2. **Capture for a Specific Duration**: Use the `timeout` command to capture for a specific period:
```bash
sudo timeout 60 tcpdump -i eth0
```


---

### **Step 11: Analyze Protocols in the Capture**

TCPDump allows you to view detailed protocol information. For example, you can see the breakdown of TCP conversations or the distribution of packets across different protocols.

1. **Show Protocol Statistics**:
```bash
sudo tcpdump -i eth0 -z stats
```

2. **Show TCP Conversations**:
```bash
sudo tcpdump -i eth0 -z conv,tcp
```

---

### **Step 12: Exporting Packets to Different Formats**

You can export captured packets in formats other than PCAP.

1. **Convert to CSV Format**: You can extract specific fields (e.g., source IP, destination IP, and port) into a CSV file:
```bash
sudo tcpdump -r capture.pcap -T fields -e ip.src -e ip.dst -e tcp.port -E header=y -E separator=, > capture.csv
```

---

### **Conclusion**

TCPDump is a versatile and powerful tool for capturing and analyzing network traffic directly from the command line. With the ability to apply advanced filters, analyze protocols, and save captures, it's invaluable for network troubleshooting, security monitoring, and forensic analysis.

By following this guide, you should be able to use TCPDump effectively for your packet capturing and network analysis needs. Don't hesitate to experiment with filters and options to tailor the tool to your specific requirements!
