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

**Given Network Address:** 10.0.0.0/24  
**Subnet Mask:** 255.255.255.0  
**Total Hosts:** 256  

To create 4 subnets, 2 bits are borrowed from the host portion. (2^2 = 4 subnets)  
**New subnet prefix:** /26  
**New subnet mask:** 255.255.255.192  

## Subnet Table

| Subnet | Network Address | First Host | Last Host | Broadcast |
|------|------|------|------|------|
| Subnet 1 | 10.0.0.0 | 10.0.0.1 | 10.0.0.62 | 10.0.0.63 |
| Subnet 2 | 10.0.0.64 | 10.0.0.65 | 10.0.0.126 | 10.0.0.127 |
| Subnet 3 | 10.0.0.128 | 10.0.0.129 | 10.0.0.190 | 10.0.0.191 |
| Subnet 4 | 10.0.0.192 | 10.0.0.193 | 10.0.0.254 | 10.0.0.255 |

Each subnet supports 62 usable host addresses.

---

## **Packet Tracer Implementation:**

The network devices were connected in the following topology:
 - 2 Routers
 - 4 Switches (1 per subnet)
 - 8 PCs (2 per subnet)

<img width="751" height="660" alt="subnet" src="https://github.com/user-attachments/assets/30b32912-dbaa-46c6-98cd-a1e221e22620" />
<br>
**IP Address Assignment:**

| Subnet | Device | IP Address | Subnet Mask | Default Gateway |
|------|------|------|------|------|
| Subnet 1 | Router0 Interface | 10.0.0.1 | 255.255.255.192 | — |
| Subnet 1 | PC0 | 10.0.0.10 | 255.255.255.192 | 10.0.0.1 |
| Subnet 1 | PC1 | 10.0.0.20 | 255.255.255.192 | 10.0.0.1 |
| Subnet 2 | Router0 Interface | 10.0.0.65 | 255.255.255.192 | — |
| Subnet 2 | PC2 | 10.0.0.70 | 255.255.255.192 | 10.0.0.65 |
| Subnet 2 | PC3 | 10.0.0.80 | 255.255.255.192 | 10.0.0.65 |
| Subnet 3 | Router1 Interface | 10.0.0.129 | 255.255.255.192 | — |
| Subnet 3 | PC4 | 10.0.0.130 | 255.255.255.192 | 10.0.0.129 |
| Subnet 3 | PC5 | 10.0.0.140 | 255.255.255.192 | 10.0.0.129 |
| Subnet 4 | Router1 Interface | 10.0.0.193 | 255.255.255.192 | — |
| Subnet 4 | PC6 | 10.0.0.200 | 255.255.255.192 | 10.0.0.193 |
| Subnet 4 | PC7 | 10.0.0.210 | 255.255.255.192 | 10.0.0.193 |

**Router Configuration:**
Router0 Configuration:
```bash
enable
configure terminal
```
```bash
interface fa0/0
ip address 10.0.0.1 255.255.255.192
no shutdown
```
```bash
interface fa0/1
ip address 10.0.0.65 255.255.255.192
no shutdown
```
```bash
interface fa0/2
ip address 192.168.1.1 255.255.255.252
no shutdown
```
**Router1 Configuration:**
```bash
enable
configure terminal
```
```bash
interface fa0/0
ip address 10.0.0.129 255.255.255.192
no shutdown
```
```bash
interface fa0/1
ip address 10.0.0.193 255.255.255.192
no shutdown
```
```bash
interface fa0/2
ip address 192.168.1.2 255.255.255.252
no shutdown
```

**Static Routing Configuration:**

To enable communication between all subnets:

Router0:
```bash
ip route 10.0.0.128 255.255.255.192 192.168.1.2
ip route 10.0.0.192 255.255.255.192 192.168.1.2
```
Router1:
```bash
ip route 10.0.0.0 255.255.255.192 192.168.1.1
ip route 10.0.0.64 255.255.255.192 192.168.1.1
```

**Verification:**
Connectivity was tested using the `ping` command.

Example:
```bash
ping 10.0.0.130
ping 10.0.0.200
```

Successful replies confirm that routing between different subnets is working correctly.

Ping status within subnet:<br>
<img width="455" height="222" alt="subnet_ping_within" src="https://github.com/user-attachments/assets/5515fd34-ad05-4238-a787-6fde1034c65c" />

Ping status between different subnets:<br>
<img width="466" height="225" alt="subnet_ping" src="https://github.com/user-attachments/assets/b2566a6c-19c5-45b7-8599-3f4d062a5321" />

The network 10.0.0.0/24 was successfully divided into 4 equal subnets using a /26 subnet mask.  
All devices were assigned valid IP addresses, and communication between different subnets was verified using static routing.


**4. You are given three IP addresses: 192.168.10.5, 172.20.15.1, and 8.8.8.8.
Identify the class of each IP address.
Determine if it is private or public.
Explain how NAT would handle a private IP when accessing the internet.**

# IP Address Classification and NAT Explanation

Given IP Addresses: 
- 192.168.10.5  
- 172.20.15.1  
- 8.8.8.8  

IP addresses are divided into classes based on their first octet:

| Class | Range |
|------|------|
| Class A | 1 – 126 |
| Class B | 128 – 191 |
| Class C | 192 – 223 |

**IP Address classification:**

| IP Address     | Class |
|---------------|--------|
| 192.168.10.5  | Class C |
| 172.20.15.1   | Class B |
| 8.8.8.8       | Class A | 

Private IP Ranges:

| Class   | Private Range |
|---------|---------------|
| Class A | 10.0.0.0 – 10.255.255.255 |
| Class B | 172.16.0.0 – 172.31.255.255 |
| Class C | 192.168.0.0 – 192.168.255.255 |

| IP Address    | Private/Public | Range |
|---------------|----------------|--------|
| 192.168.10.5  | Private        | Falls within 192.168.0.0 – 192.168.255.255 |
| 172.20.15.1   | Private        | Falls within 172.16.0.0 – 172.31.255.255 |
| 8.8.8.8       | Public         | Not in any private IP range |


**NAT (Network Address Translation):** 
NAT is a technique used by routers to translate private IP addresses into a public IP address so devices can access the internet.

Let us consider an example scenario:<br>
A device with private IP:
```
192.168.10.5
```
wants to access:
```
8.8.8.8
```
Private IP addresses cannot directly access the internet and require NAT for communication. It is performed by the router.

NAT Procedure:
1. The PC sends a request to the router.
2. The router replaces the source private IP with its public IP.
3. The request is sent to the internet.
4. The destination (e.g., 8.8.8.8) responds to the public IP.
5. The router translates the response back to the original private IP.
6. The PC receives the response.

| Original Packet | Translated Packet |
|----------------|------------------|
| Source: 192.168.10.5 | Source: Public IP (e.g., 200.1.1.1) |
| Destination: 8.8.8.8 | Destination: 8.8.8.8 |


**5. In Cisco Packet Tracer, configure NAT on a router to allow internal devices (192.168.1.x) to access the internet.
Test connectivity by pinging an external public IP.
Capture the traffic in Wireshark and analyze the source IP before and after NAT translation.**

A network is built in Cisco Packet Tracer consisting of:
- 1 Router
- 1 Switch
- 2 PCs (Internal Network)
- 1 Server (Simulated Internet)

<img width="316" height="540" alt="nat_topology" src="https://github.com/user-attachments/assets/e625f8b9-0fcc-43cd-b600-0a6595e53ee0" />

**IP Addressing:**

| Device | Interface | IP Address | Subnet Mask | Description |
|-------|----------|------------|-------------|------------|
| Router | Fa0/0 | 192.168.1.1 | 255.255.255.0 | Internal (LAN) |
| Router | Fa0/1 | 200.0.0.1 | 255.255.255.0 | External (WAN) |
| PC0 | FastEthernet0 | 192.168.1.2 | 255.255.255.0 | Internal Host |
| PC1 | FastEthernet0 | 192.168.1.3 | 255.255.255.0 | Internal Host |
| Server | FastEthernet0 | 200.0.0.2 | 255.255.255.0 | Public Server |

Default Gateway (PCs): 192.168.1.1

**Router Configuration:**
Enable NAT and Configure Interfaces:
```bash
enable
configure terminal
```
```bash
interface fa0/0
ip address 192.168.1.1 255.255.255.0
ip nat inside
no shutdown
```
```bash
interface fa0/1
ip address 200.0.0.1 255.255.255.0
ip nat outside
no shutdown
```

**NAT Configuration (PAT):**
Create Access List:
```bash
access-list 1 permit 192.168.1.0 0.0.0.255
```
Enable NAT Overload:
```bash
ip nat inside source list 1 interface fa0/1 overload
```

**Verification:**
Ping Test (from PC)
```bash
ping 200.0.0.2
```
<img width="636" height="565" alt="nat_ping" src="https://github.com/user-attachments/assets/6bfb929e-197b-483e-9162-86fa6227a7c8" />

Successful reply indicates NAT is working

On Router:
```bash
show ip nat translations
```

Expected output:
```
Inside global    Inside local      Outside local     Outside global
200.0.0.1        192.168.1.2       200.0.0.2         200.0.0.2
```

Wireshark Analysis: 
   1. Open Simulation Mode in Packet Tracer
   2. Filter: ICMP
   3. Start capture
   4. Ping from PC to Server
   5. Observe packet flow

<img width="937" height="532" alt="nat_simulation" src="https://github.com/user-attachments/assets/cb052e08-f12b-4aa6-b1dc-2c87f490d701" />

<img width="287" height="518" alt="nat_simulation_2" src="https://github.com/user-attachments/assets/e329e598-f6ff-4079-ac6a-7ae5dd190eb5" />

**Packet Analysis:**

Before NAT (Inside Network):
- Source IP: 192.168.1.2
- Destination IP: 200.0.0.2

After NAT (Outside Network):
- Source IP: 200.0.0.1
- Destination IP: 200.0.0.2

<img width="565" height="308" alt="nat_router" src="https://github.com/user-attachments/assets/b28a8acd-2a2e-4032-9354-f1b03d2c9ffe" />

NAT Translation:

| Stage | Source IP | Destination IP |
|------|----------|----------------|
| Before NAT | 192.168.1.2 | 200.0.0.2 |
| After NAT | 200.0.0.1 | 200.0.0.2 |

NAT was successfully configured using PAT. Internal devices were able to access external networks. Wireshark analysis confirmed that private IP addresses were translated into a public IP address.

---

