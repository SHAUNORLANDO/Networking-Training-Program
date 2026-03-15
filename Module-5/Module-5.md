**Networking Assessment - Module-5**

**1) Capture and analyze ARP packets using Wireshark. Inspect the ARP request and reply frames, and discuss the role of the sender's IP and MAC address in these packets.**

Applied 'arp' filter in Wireshark.
Created traffic using 'ping' command in the terminal:
```bash
ping 192.168.1.1
```
We can find two packets captured:
- ARP request
- ARP reply

**ARP Request:**

This request is broadcasted to all devices in the network to find the MAC address of the device with IP `192.168.1.8`.


2) Using Packet Tracer, simulate an ARP spoofing attack. Analyze the behavior of devices on the network when they receive a malicious ARP response.


3) Manually configure static IPs on the client devices(like Pc or your mobile phone) and verify connectivity using ping.


4) Use Wireshark to capture DHCP Discover, Offer, Request, and Acknowledge messages and explain the process.


5) Given an IP address range of 192.168.1.0/24, divide the network into 4 subnets.
Task: Manually calculate the new subnet mask and the range of valid IP addresses for each subnet.
Assign IP addresses from these subnets to devices in Cisco Packet Tracer and verify connectivity using ping between them.


6) You are given three IP addresses: 10.1.1.1, 172.16.5.10, and 192.168.1.5.
Task: Identify the class of each IP address (Class A, B, or C). What is the default subnet mask for each class?
Provide the range of IP addresses for each class.


7) In Cisco Packet Tracer, create a small network with multiple devices (e.g., 2 PCs and a router). Use private IP addresses (e.g., 192.168.1.x) on the PCs and configure the router to perform NAT to allow the PCs to access the internet.
Task: Test the NAT configuration by pinging an external IP address from the PCs and capture the traffic using Wireshark.
What is the source IP address before and after NAT?
Note:
For each task, submit screenshots of your configurations, ping tests, or Wireshark captures.
Provide a brief explanation of the concepts involved in each task and how the configurations and tests were performed.
