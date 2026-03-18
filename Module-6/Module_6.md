# Module 6 Assignment - Layer 3

**1. Capture and analyze ARP packets using Wireshark. Inspect the ARP request and reply frames when your device attempts to find the router's MAC address.
Discuss the importance of ARP in packet forwarding.**

## Q1: ARP Packet Capture and Analysis using Wireshark

Opened Wireshark and selected the active network interface and started packet capture.
Applied arp filter.

Opened terminal and executed:
```bash
   ping 192.168.1.1
```

Captured the following ARP packets:
 - ARP Request
 - ARP Reply
<img width="1098" height="151" alt="arp_1" src="https://github.com/user-attachments/assets/8eb318f9-a112-4b2c-b687-4533a1349378" />
<br>

#### ARP Request:
The device sends a broadcast message asking for the MAC address of the router.
Message: "Who has 192.168.1.9? Tell 192.168.1.1"
<img width="1872" height="730" alt="arp_req" src="https://github.com/user-attachments/assets/5dfeffd8-7350-436d-afa3-39c4ced9c49b" />
<br>

#### ARP Reply:
The router responds with its MAC address.
Message: "192.168.1.9 is at 34:2e:b7:94:b7:9f"
<img width="1918" height="725" alt="arp_reply" src="https://github.com/user-attachments/assets/71fee7bc-4bea-4feb-9328-b3dd799d6822" />
<br>

**Importance of ARP in Packet Forwarding:**
ARP (Address Resolution Protocol) is essential for communication within a local network.
- Devices use IP addresses at the network layer.
- Data transmission at the data link layer requires MAC addresses.
- ARP maps IP addresses to MAC addresses.
- Without ARP, devices cannot determine the destination MAC address and packets cannot be delivered within the network.
- With help of ARP, proper IP-to-MAC mapping occurs and packets are forwarded successfully.
---

**2. Manually configure static routes on a router to direct packets to different subnets.
Use the ip route command and verify connectivity using ping and traceroute.**


**3. Given a network address of 10.0.0.0/24, divide it into 4 equal subnets.
Calculate the new subnet mask.
Determine the valid host range for each subnet.
Assign IP addresses to devices in Packet Tracer and verify connectivity.**


**4. You are given three IP addresses: 192.168.10.5, 172.20.15.1, and 8.8.8.8.
Identify the class of each IP address.
Determine if it is private or public.
Explain how NAT would handle a private IP when accessing the internet.**

**5. In Cisco Packet Tracer, configure NAT on a router to allow internal devices (192.168.1.x) to access the internet.
Test connectivity by pinging an external public IP.
Capture the traffic in Wireshark and analyze the source IP before and after NAT translation.**
