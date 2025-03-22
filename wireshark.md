### **Wireshark Guide: Basic Usage and Network Analysis**

---

### **Prerequisites**

1. **Wireshark Installation**: Ensure that Wireshark is installed on your Linux or Windows machine.
2. **Permissions**: You may need administrator or root permissions to capture network packets.
3. **Network Interface**: You should know the network interface you will be using to capture packets (e.g., `eth0`, `wlan0`, etc.).
4. **Network Traffic**: If you're using Wireshark to troubleshoot or analyze network activity, ensure you have traffic flowing on the network.

---

### **Step 1: Install Wireshark**

#### **For Linux (Ubuntu/Debian-based distributions)**

1. **Update the package list**:
```bash
sudo apt update
```

2. **Install Wireshark**:
```bash
sudo apt install wireshark
```

2. **Grant Non-Root Access to Wireshark** (optional but recommended):

 During installation, you might be prompted to allow non-superusers to capture packets. If not, add your user to the `wireshark` group:
```bash
sudo usermod -aG wireshark $(whoami)
```

   Log out and log back in to apply the group changes.

3. **Verify Installation**:
```bash
wireshark --version
```

#### **For Windows**

1. Download the Wireshark installer from the Wireshark download page.
2. Run the installer and follow the instructions to install Wireshark.

---

### **Step 2: Start Capturing Network Traffic**

1. **Launch Wireshark**: Open Wireshark by typing `wireshark` in your terminal (Linux) or using the Wireshark icon (Windows).
    
2. **Select the Interface**:
    - Wireshark will display a list of available network interfaces (e.g., Ethernet, Wi-Fi). Select the network interface you want to capture traffic from.
    - Click on the interface to start capturing traffic.
    
    Example interfaces:
    - `eth0` for wired Ethernet
    - `wlan0` for wireless interfaces
- 
1. **Start Capturing**:
    - Click on the **"Start"** button (shaped like a shark fin) or double-click on the desired interface.
    - Wireshark will begin capturing all the packets flowing through the selected network interface.

---

### **Step 3: Analyze Captured Packets**

Once you've started capturing traffic, Wireshark will display each captured packet in real-time. Each packet will contain various details, including the protocol used, source and destination addresses, packet length, and more.

#### **Packet Details Panel**:

- **Packet List**: This panel displays a summary of all captured packets.
- **Packet Details**: Displays detailed information about the currently selected packet.
- **Packet Bytes**: Displays the raw byte data of the selected packet.

---

### **Step 4: Filter Network Traffic**

Wireshark provides powerful filtering capabilities that allow you to narrow down the packets you're interested in.

#### **Common Display Filters**:

1. **Filter by Protocol**:

**TCP**:
```bash
tcp
```

**UDP**:
```bash
udp
```

**ICMP**:
```bash
icmp
```

2. **Filter by IP Address**:

**Source IP**:
```bash
ip.src == 192.168.1.1
```

**Destination IP**:
```bash
ip.dst == 192.168.1.1
```

3. **Filter by Port Number**:

**TCP Port 80 (HTTP)**:
```bash
tcp.port == 80
```

 **UDP Port 53 (DNS)**:
```bash
udp.port == 53
```

4. **Filter by HTTP** (to show only HTTP traffic):


5. **Combine Filters** (using `and`, `or` operators):

**Show only TCP traffic to port 80 from a specific IP**:
```bash
tcp.port == 80 and ip.src == 192.168.1.100
```

---

### **Step 5: Inspect Packets in Detail**

1. **Select a Packet**: Click on any packet in the packet list to view its detailed information.
2. **Expand Protocol Layers**: Protocols (e.g., Ethernet, IP, TCP) are displayed in a tree structure. You can expand each protocol layer to view additional details, such as source and destination IP addresses, ports, and flags.

---

### **Step 6: Follow Streams**

Wireshark allows you to follow a complete TCP or UDP stream to view the entire conversation between two hosts.

1. **Right-click on a Packet**: Right-click on any packet that is part of a conversation you want to track.
2. **Select "Follow" > "TCP Stream" or "UDP Stream"**: This will display the entire conversation, making it easier to analyze the flow of data.

---

### **Step 7: Save and Export Captured Data**

1. **Save Capture File**:
    
    - Go to **File > Save As** and choose a location to save your capture file.
    - The capture file is saved in **pcapng** or **pcap** format, which can be loaded into Wireshark later for analysis.
2. **Export Packet Data**:
    
    - You can export packet data to various formats, such as CSV, XML, or plain text, for further analysis or documentation.
    - Go to **File > Export Packet Dissections** and choose the export format.

---

### **Step 8: Analyze and Troubleshoot Network Issues**

Wireshark is a great tool for diagnosing network issues. Here are some common problems you can troubleshoot using Wireshark:

1. **Latency Issues**:
    
    - Filter for `icmp` traffic and check for any packet loss or delayed responses (ping).
2. **TCP Connection Issues**:
    
    - Filter for `tcp` traffic and check for retransmissions, which may indicate issues with packet delivery.
3. **DNS Issues**:
    
    - Filter for `udp.port == 53` to view DNS queries and responses, helping you identify DNS resolution issues.
4. **Suspicious Activity**:
    
    - Look for unusual ports or traffic that could be indicative of security breaches (e.g., non-standard ports or unexpected traffic flows).

---

### **Step 9: Advanced Wireshark Features**

1. **Statistics**:
    
    - Use **Statistics > Summary** to view overall statistics about the capture file, such as packet counts, protocol breakdown, and traffic duration.
2. **IO Graphs**:
    
    - **Statistics > I/O Graphs** allows you to visualize network traffic over time, helping you identify spikes or unusual patterns.
3. **Expert Info**:
    
    - **Analyze > Expert Information** provides a summary of important events or anomalies detected in the capture, such as retransmissions or checksum errors.

---

### **Step 10: Stop Capture and Analyze Data**

1. **Stop Capture**: Click on the red square (Stop) button to stop capturing packets once you have gathered enough data.
2. **Review and Investigate**: Go through the captured packets, apply filters, and use Wireshark's analysis tools to gain insights into your network traffic.

---

### **Conclusion**

Wireshark is a powerful tool for monitoring and analyzing network traffic. Whether you're troubleshooting network issues, investigating security incidents, or simply learning about network protocols, Wireshark provides detailed insights into the packets flowing through your network.

By following the steps in this guide, you can begin using Wireshark for network analysis and gain valuable data about your network's behavior.
