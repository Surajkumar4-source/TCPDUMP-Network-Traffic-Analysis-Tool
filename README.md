# TCPDUMP: Network Traffic Analysis 

<br>

## Introduction

`tcpdump` is a powerful command-line packet sniffer and analyzer tool widely used by network administrators and security professionals. It captures and filters network packets, providing a detailed insight into TCP/IP activity on a specific interface. `tcpdump` is particularly useful for diagnosing network issues, monitoring traffic, and troubleshooting applications that communicate over the network.

## How tcpdump Works

At its core, `tcpdump` uses the libpcap library to intercept and analyze packets from the network stack. These packets can belong to different protocols, such as TCP, UDP, or ICMP, and they are either incoming or outgoing traffic on your machine.

## Key Features:
- Captures packets on specific network interfaces.
- Filters traffic by protocols, IP addresses, ports, or other criteria.
- Saves captured traffic into files for offline analysis using tools like Wireshark.
- Provides both high-level and detailed packet analysis in HEX or ASCII formats.

## Installation

Before using `tcpdump`, ensure it is installed on your Linux system. Follow these steps based on your distribution:

### For Debian/Ubuntu-based Systems:
```bash
sudo apt update
sudo apt install tcpdump
```

### For RHEL/CentOS/Fedora-based Systems:
```bash

sudo yum install tcpdump

```

### Verify Installation:
  - Run the following command to confirm installation:

```bash

tcpdump --version
```

<br>
<br>



## Common Use Cases and Commands

### 1. List All Available Interfaces
```bash

tcpdump -D
```
  - Explanation: Displays the list of all available interfaces. Use the desired interface in subsequent commands.

### 2. Capture Packets on a Specific Interface
```bash

tcpdump -i ens33
```
  - Explanation: Captures all packets from the ens33 interface.

### 3. Limit the Number of Packets Captured
```bash

tcpdump -c 5 -i ens33
```
  - Explanation: Captures only 5 packets from the ens33 interface.

### 4. Display Packets in ASCII Format
```bash

tcpdump -A -i ens33
```
  - Explanation: Converts packet content to ASCII format for better readability (e.g., plain text content).

### 5. Display Packets in HEX and ASCII
```bash

tcpdump -XX -i ens33
```
  - Explanation: Displays packet content in both HEX and ASCII for detailed analysis.

### 6. Save Captured Packets to a File
```bash

tcpdump -w packets.pcap -i ens33
```
  - Explanation: Saves captured packets to packets.pcap for offline analysis.

### 7. Read Captured Packets from a File
```bash

tcpdump -r packets.pcap
```
  - Explanation: Reads and displays the contents of a previously saved .pcap file.

### 8. Filter by IP Address
  - Source IP:
```bash

tcpdump -i ens33 src x.x.x.x
```
 - Explanation: Captures packets originating from the source IP x.x.x.x.

  - Destination IP:
```bash

tcpdump -i ens33 dst x.x.x.x
```
  - Explanation: Captures packets destined for the IP x.x.x.x.

### 9. Filter by Port
```bash

tcpdump -i ens33 port 22
```
- Explanation: Captures packets associated with port 22 (commonly used for SSH).

### 10. Capture Only TCP Packets
```bash

tcpdump -i ens33 tcp
```
 - Explanation: Filters traffic to capture only TCP packets.

### 11. Capture Packets on All Interfaces
```bash

tcpdump -i any
```
  - Explanation: Captures packets across all interfaces.

### 12. Capture Specific Host Traffic
```bash

tcpdump -i ens33 host x.x.x.x
```
  - Explanation: Captures all packets to or from the host x.x.x.x.

13. Use Complex Filters
```bash

tcpdump -i lo "port 80 and (src 192.168.1.1 or src 10.0.0.1)"
```
  - Explanation: Captures traffic on port 80 from source IPs 192.168.1.1 or 10.0.0.1.


<br>
<br>







## Assignments  

### 1. Detecting Network Latency Issues
  - Task: Capture all ICMP packets (used by ping) to analyze network latency.

```bash

tcpdump -i ens33 icmp
```
  - Objective: Identify delayed or lost ICMP packets to troubleshoot network delays.

### 2. Monitoring HTTP/HTTPS Traffic
  - Task: Capture and inspect HTTP requests and responses on a server.

```bash

tcpdump -i ens33 port 80
```
   - Objective: Monitor incoming and outgoing web traffic for debugging or security analysis.

- To monitor encrypted HTTPS traffic:

```bash
tcpdump -i ens33 port 443
```
### 3. Identifying Unauthorized Access Attempts
  - Task: Capture packets on SSH port (22) to detect unauthorized login attempts.

```bash
tcpdump -i ens33 port 22
```
 - Objective: Analyze packets for brute-force attacks or unexpected SSH activity.

### 4. Analyzing Traffic from a Specific Subnet
  - Task: Monitor all traffic to or from a specific subnet (e.g., 192.168.1.0/24).

```bash
tcpdump -i ens33 net 192.168.1.0/24
```
  - Objective: Filter traffic within a subnet to understand internal network behavior.

### 5. Capture DNS Queries for Troubleshooting
  - Task: Capture and inspect DNS queries and responses.

```bash
tcpdump -i ens33 port 53
```
  - Objective: Diagnose DNS-related issues such as slow name resolution or DNS spoofing attacks.

### 6. Capturing Specific Protocol Traffic
  - Task: Capture only UDP packets for protocol-specific analysis.

```bash
tcpdump -i ens33 udp
```
  - Objective: Troubleshoot applications that use UDP, such as video streaming or VoIP.

### 7. Extracting File Transfers (FTP)
  - Task: Monitor and capture FTP traffic (port 21).

```bash
tcpdump -i ens33 port 21
```
  - Objective: Inspect FTP sessions for troubleshooting file transfer issues or detecting unauthorized transfers.

### 8. Analyzing Packet Loss
  - Task: Capture traffic to analyze packet loss during a file download or upload.

```bash
tcpdump -i ens33 host x.x.x.x
```
  - Objective: Evaluate traffic between your machine and a remote server to identify dropped packets.

### 9. Detecting Malicious Activity
  - Task: Monitor traffic for abnormal activity, such as scanning or unauthorized access attempts.

```bash
tcpdump -i ens33 "tcp[tcpflags] & tcp-syn != 0 and tcp[tcpflags] & tcp-ack == 0"
```
  - Objective: Detect SYN packets without ACK, a common indicator of port scans.

### 10. Inspecting ARP Traffic
  - Task: Capture ARP packets to detect spoofing attempts or troubleshoot ARP table issues.

```bash
tcpdump -i ens33 arp
```
  - Objective: Monitor ARP activity to detect potential MITM (Man-in-the-Middle) attacks.

### 11. Saving Long-Term Network Logs
  - Task: Save all traffic to a file for later analysis over an extended period.
```bash
tcpdump -i ens33 -w long_capture.
```
  - Objective: Capture network logs for offline analysis using tools like Wireshark.

### 12. Diagnosing Application-Specific Issues
  - Scenario: A web application is experiencing delays. Capture only traffic to/from the application's server (IP 10.0.0.1) on port 8080.

```bash
tcpdump -i ens33 host 10.0.0.1 and port 8080
```
  - Objective: Pinpoint bottlenecks in application-layer traffic.

### 13. Capturing VoIP Traffic
  - Task: Capture RTP (Real-Time Protocol) packets for VoIP analysis.

```bash
tcpdump -i ens33 udp and portrange 10000-20000
```
  - Objective: Analyze voice or video communication traffic for quality or troubleshooting.

### 14. Verifying Network Security Rules
  - Task: Test firewall or security group configurations by monitoring blocked or allowed traffic.

```bash
tcpdump -i ens33 host x.x.x.x and port 80
```
  - Objective: Verify that the firewall rules are correctly permitting or denying traffic.

### 15. Detecting DDoS Attacks
  - Scenario: Capture and analyze high volumes of incoming packets to detect a Distributed Denial-of-Service (DDoS) attack.

```bash
tcpdump -n -i ens33 "tcp and (port 80 or port 443)"
```
  - Objective: Identify unusual spikes in HTTP/HTTPS traffic.





<br>
<br>


## Conclusion

*While implementing these practical use cases with tcpdump, I gained valuable insights into network traffic analysis and its significance in real-world scenarios. Here's a summary of the learnings:*

1. Deep Understanding of Network Layers:

  - I learned how different protocols (HTTP, SSH, DNS, etc.) communicate within the network and how to monitor their specific behavior using filters.

2. Practical Debugging Skills:

  - Debugging HTTP requests and responses provided clarity on how applications communicate over the network, helping me understand how to trace issues like delays or misconfigurations.

3. Enhanced Security Awareness:

  - Monitoring for suspicious activities (like brute force attempts or unauthorized access) helped me realize the importance of proactive security analysis in identifying potential threats.

4. Efficient Troubleshooting:

  - By capturing dropped packets and analyzing delays, I improved my ability to diagnose and resolve network performance issues effectively.

5. Traffic Filtering Mastery:

  - Filtering traffic based on IPs, ports, and protocols taught me how to focus on relevant data, reducing noise and making analysis more efficient.

6. Tool Proficiency:

  - Working with tcpdump reinforced my skills in using powerful network diagnostic tools and highlighted the importance of saving and analyzing .pcap files with complementary tools like Wireshark for deeper insights.

<br>
<br>


*This implementation not only improved my technical understanding but also emphasized the importance of network monitoring for maintaining robust, secure, and well-functioning systems.*









<br>
<br>
<br>
<br>



**👨‍💻 𝓒𝓻𝓪𝓯𝓽𝓮𝓭 𝓫𝔂**: [Suraj Kumar Choudhary](https://github.com/Surajkumar4-source) | 📩 **𝓕𝓮𝓮𝓵 𝓯𝓻𝓮𝓮 𝓽𝓸 𝓓𝓜 𝓯𝓸𝓻 𝓪𝓷𝔂 𝓱𝓮𝓵𝓹**: [csuraj982@gmail.com](mailto:csuraj982@gmail.com)





<br>


