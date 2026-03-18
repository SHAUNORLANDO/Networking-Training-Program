# Module 6 Assignment - Layer 3

**1. Capture and analyze ARP packets using Wireshark. Inspect the ARP request and reply frames when your device attempts to find the router's MAC address.
Discuss the importance of ARP in packet forwarding.**

## Q1: ARP Packet Capture and Analysis using Wireshark

Opened Wireshark and selected the active network interface and started packet capture.
Applied arp filter.

Opened terminal and executed:
```bash
   ping 192.168.1.9
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

The network topology constructed in Cisco Packet Tracer consists of:
- 2 Routers
- 2 Switches
- 4 PCs

Each router connects to:
- One LAN (via switch)
- One inter-router link

<img width="593" height="473" alt="static_route_topology" src="https://github.com/user-attachments/assets/4cfae70d-ffea-4c79-90cc-16c3317a496e" />

**IP Addressing Table:**

| Device    | Interface        | IP Address        | Subnet Mask       | Gateway          |
|----------|------------------|------------------|------------------|------------------|
| Router0  | Fa0/0 (LAN)      | 192.168.2.3      | 255.255.255.0    | -                |
| Router0  | Fa0/1 (WAN)      | 192.168.1.2      | 255.255.255.0    | -                |
| Router1  | Fa0/0 (LAN)      | 192.168.3.3      | 255.255.255.0    | -                |
| Router1  | Fa0/1 (WAN)      | 192.168.1.4      | 255.255.255.0    | -                |
| PC0      | FastEthernet0    | 192.168.2.7      | 255.255.255.0    | 192.168.2.3      |
| PC1      | FastEthernet0    | 192.168.2.9      | 255.255.255.0    | 192.168.2.3      |
| PC2      | FastEthernet0    | 192.168.3.5      | 255.255.255.0    | 192.168.3.3      |
| PC3      | FastEthernet0    | 192.168.3.7      | 255.255.255.0    | 192.168.3.3      |

**Router Configuration:**
Router0:
```
enable
configure terminal

interface fa0/0
ip address 192.168.2.3 255.255.255.0
no shutdown

interface fa0/1
ip address 192.168.1.2 255.255.255.0
no shutdown
```
Router1:
```
enable
configure terminal

interface fa0/0
ip address 192.168.1.4 255.255.255.0
no shutdown

interface fa0/1
ip address 192.168.3.3 255.255.255.0
no shutdown
```

**Static Route Configuration:**
Router0:
```
ip route 192.168.3.0 255.255.255.0 192.168.1.4
```
Router1:
```
ip route 192.168.2.0 255.255.255.0 192.168.1.2
```

To check interface status:
```
show ip interface brief
```
<img width="576" height="205" alt="static_route_ip" src="https://github.com/user-attachments/assets/506ec876-f9ac-4221-a100-973d248f3034" />
<br>
All interfaces are `up/up`

**Ping Test:**

From PC0:
```
ping 192.168.3.5
ping 192.168.3.7
```

From PC2:
```
ping 192.168.2.7
ping 192.168.2.9
```

All pings are successful.
Example: <br> 
<img width="621" height="557" alt="static_route_ping" src="https://github.com/user-attachments/assets/3f8db8f6-2cd6-4835-81ef-9f8c602d0f6b" />
<br>

**Traceroute Test:**
From PC1:
```
tracert 192.168.3.7
```
<img width="633" height="565" alt="static_route_tracert" src="https://github.com/user-attachments/assets/80f1f0a4-52d6-4858-9718-797b8c9d3640" />
<br>

Static routing was successfully configured between the two routers.  
Devices in different subnets were able to communicate with each other, verified using `ping` and `traceroute`.

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
