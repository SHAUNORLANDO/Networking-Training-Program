# Networking Training Program - Module 7 and 8 Assignment

**1. Try Test-Connection and nslookup commands for below websites: <br>
www.google.com <br>
www.facebook.com <br>
www.amazon.com <br>
www.github.com <br>
www.cisco.com <br>**

**Test-Connection command:**
The `Test-Connection` command is used to check whether a system can reach a particular website or server over the network. It sends ICMP echo requests (similar to ping) and verifies if a response is received.

This helps in:
- Checking internet connectivity
- Measuring network reliability
- Identifying packet loss or delays

The following commands were executed in PowerShell:
```bash
Test-Connection www.google.com
Test-Connection www.facebook.com
Test-Connection www.amazon.com
Test-Connection www.github.com
Test-Connection www.cisco.com
```

<img width="822" height="917" alt="1 1" src="https://github.com/user-attachments/assets/c5008145-16c7-44b0-a840-6012c4fb8c71" />

- **Source** → The local system from which the request is sent  
- **Destination** → The website or server being tested  
- **IPv4Address** → The IP address of the destination server
Several packets were sent and responses were received successfully.

**nslookup command:**
The `nslookup` command is used to find the IP address of a domain name. It queries the DNS (Domain Name System) server and translates a  website name into its corresponding IP address.

This helps in:
- Understanding DNS resolution
- Identifying the DNS server being used
- Checking if a domain is properly mapped

The following commands were executed:
```bash
nslookup www.google.com
nslookup www.facebook.com
nslookup www.amazon.com
nslookup www.github.com
nslookup www.cisco.com
```

<img width="506" height="957" alt="1 2" src="https://github.com/user-attachments/assets/bd552e19-b8fd-4d07-b168-b3e25347ad61" />


- **Server** → The DNS server used for resolving the domain (in this case, the local router)  
- **Address** → The IP address of the DNS server  
- **Non-authoritative answer** → Indicates that the response is from a cached DNS server  
- **Name** → The domain name queried  
- **Addresses** → The resolved IP addresses (both IPv4 and IPv6)  

---

**2. Use Wireshark to capture and analyze DNS, TCP, UDP traffic and packet header, packet flow, options and flags**

In Wireshark, selected the active network interface (Wi-Fi) and started packet capture.
Opened a web browser and visited google.com.
Stopped the capture after a few seconds and applied filters to analyze different types of traffic.

**DNS:**
Filter used:
```bash
dns
```
<img width="1918" height="697" alt="2 1" src="https://github.com/user-attachments/assets/1ae778f7-a985-48b2-b4c4-84accc4c8ef4" />
<img width="1918" height="743" alt="2 2" src="https://github.com/user-attachments/assets/038bd52e-e9b5-4bdd-953e-047d5f499942" />

- DNS queries and responses were observed.
- Domain names were translated into IP addresses.

**TCP**
Filter used:
```
tcp
```
<img width="1918" height="847" alt="2 3" src="https://github.com/user-attachments/assets/5a14ffd6-9401-431c-bbef-51ed6e9fcefa" />
<img width="1918" height="855" alt="2 4" src="https://github.com/user-attachments/assets/10e9a88c-b242-40cb-81ae-3ed3f64d52a8" />
<img width="1918" height="887" alt="2 5" src="https://github.com/user-attachments/assets/7552cd4f-36e2-4d32-91fb-5bef731158e4" />
<img width="1918" height="851" alt="2 6" src="https://github.com/user-attachments/assets/388a8636-171d-4780-a75a-736b0159820a" />
<img width="1918" height="870" alt="2 7" src="https://github.com/user-attachments/assets/230dc3b7-f451-46fe-ad1b-c817270057fc" />

- TCP packets showed a 3-way handshake process:
  - SYN
  - SYN-ACK
  - ACK
- This confirms reliable connection establishment.

**UDP**
Filter used:
```
udp
```
<img width="1918" height="743" alt="2 8" src="https://github.com/user-attachments/assets/5a934c92-b94a-4bca-bfe2-ef06857c6aca" />
<img width="1918" height="815" alt="2 9" src="https://github.com/user-attachments/assets/e4850046-3608-418b-abde-32eb823aac84" />

- UDP packets were observed without any handshake.
- DNS queries primarily used UDP protocol.
- Faster but less reliable compared to TCP.

---

**3. Explore traceroute/tracert for different websites eg:google.com and analyse the parameters in the output and explore different options for traceroute command**

The `tracert` (Windows) or `traceroute` (Linux) command is used to track the route that data packets take to reach a destination.

- Traceroute relies on ICMP responses, and works by sending packets with increasing Time-To-Live (TTL) values and records each intermediate router (hop) along the path.

The following commands were executed:
```bash
tracert www.google.com
tracert www.github.com
```
<img width="623" height="283" alt="3 1" src="https://github.com/user-attachments/assets/c159a7ad-cfef-4fd8-a05b-fdd272493863" />
<img width="627" height="498" alt="3 2" src="https://github.com/user-attachments/assets/5140201c-930a-41a2-845c-b46609ce6978" />
<br>
Additional options explored:

```bash
tracert -d www.google.com
tracert -h 5 www.google.com
```
<img width="628" height="597" alt="3 3" src="https://github.com/user-attachments/assets/b7696dac-3b6d-4f9a-8105-f595e504fa33" />

Each line in the output represents a hop.

**Parameters:**
- **Hop Number** → Indicates the sequence of routers in the path  
- **Response Time (ms)** → Time taken for the packet to reach that hop (three attempts shown)  
- **IP Address / Hostname** → The router or server at that hop  

- The first hop corresponds to the local router (192.168.1.1).
- Intermediate hops belong to the Internet Service Provider (ISP).
- The final hop represents the destination server.
- The response time increases as the distance to the destination increases.
- Some intermediate hops showed "Request timed out". This does not indicate a network failure. It implies that those routers are configured to block or ignore ICMP requests due to security or firewall settings. Even though these hops did not respond, the final destination was reached successfully, confirming that the network path is functioning properly.
- Some hops may show `* * *`, indicating no response due to firewall or security restrictions.
- Using `-d` option speeds up the process by skipping DNS resolution.
- Using `-h` option limits the maximum number of hops (routers) the traceroute will check.

**Linux execution:**
Command:
```bash
traceroute -m 5 google.com
```

<img width="647" height="122" alt="3 4" src="https://github.com/user-attachments/assets/c2752f05-6d29-45a8-acd8-4ab2c10f98fd" />

 - -m option specifies the maximum no.of hops.

**Issue encountered:**
- While executing traceroute in Linux, a "Temporary failure in name resolution" error was encountered.
- This indicates a DNS resolution issue, where the system is unable to convert domain names into IP addresses.
- The issue was resolved by reinstalling traceroute command in the system and restarting Network Manager.
- Alternatively, traceroute can be performed using IP addresses to bypass DNS resolution. (`traceroute 8.8.8.8`)

Successfully traced the route to different websites and analyzed the parameters in the traceroute output.

---

**4. Use Cisco packet tracer for the below**

**5. Set up trunk ports between switches and try ping between different VLANs.**

Topology:
- 2 × Switches (2950)
- 4 × PCs
- 1 × Trunk link between switches

<img width="725" height="332" alt="6 1" src="https://github.com/user-attachments/assets/f3db2034-3adb-4869-82e9-bcb96a3f1999" />

**VLAN Distribution:**
- VLAN 10: PC0, PC1 (Switch0)
- VLAN 20: PC2, PC3 (Switch1)

**IP Addressing:**

| Device | IP Address     | VLAN   |
|--------|---------------|--------|
| PC0    | 192.168.10.3  | VLAN 10 |
| PC1    | 192.168.10.2  | VLAN 10 |
| PC2    | 192.168.20.3  | VLAN 20 |
| PC3    | 192.168.20.2  | VLAN 20 |

**Connections:**
- PC0 → Switch0 (Fa0/1)
- PC1 → Switch0 (Fa0/2)
- PC2 → Switch1 (Fa0/1)
- PC3 → Switch1 (Fa0/2)
- **Trunk Link:** Switch0 Fa0/24 ↔ Switch1 Fa0/24

**Configuration:**

Switch0 Configuration:
```bash
enable
conf t

vlan 10
name VLAN10

int range fa0/1-2
switchport mode access
switchport access vlan 10

interface fa0/24
switchport mode trunk

end
write memory
```

Switch 1 Configuration:
```bash
enable
conf t

vlan 20
name VLAN20

int range fa0/1-2
switchport mode access
switchport access vlan 20

interface fa0/24
switchport mode trunk

end
write memory
```

**Ping Test:**
Communication within same VLAN is Successful but between different VLANs failed:
<img width="627" height="610" alt="6 2" src="https://github.com/user-attachments/assets/a5ab6d0e-a56c-4f2d-96ed-7f4b956d9a61" />

**6. Change the native VLAN on a trunk port.Test for VLAN mismatches and troubleshoot.**

- Native VLAN carries untagged traffic on a trunk link
- Default Native VLAN = VLAN 1
- Both ends of a trunk must have the same native VLAN
- Mismatch can cause network issues and security vulnerabilities

**Configuring Native VLAN**
<br>
Switch0:
```bash
enable
conf t

vlan 99
name NATIVE_VLAN

int fa0/24
switchport mode trunk
switchport trunk native vlan 99

end
write memory
```
<img width="545" height="192" alt="6 3" src="https://github.com/user-attachments/assets/27e12769-313d-4120-9a76-c1ef22ce8032" />
<br>

Switch1:
```bash
enable
conf t

vlan 99
name NATIVE_VLAN

int fa0/24
switchport mode trunk
switchport trunk native vlan 99

end
write memory
```
<img width="542" height="188" alt="6 4" src="https://github.com/user-attachments/assets/ba4c5993-cc1b-400a-9c1d-b6cd27bea455" />
<br>

**Create VLAN Mismatch:**
Changed native VLAN on only Switch1:
```bash
conf t
int fa0/24
switchport trunk native vlan 1
end
```
<img width="518" height="72" alt="6 5" src="https://github.com/user-attachments/assets/02c85b7c-d83f-48ec-b1e0-60fff6bb6550" />

**Observations:**
Warning Message!:
%CDP-4-NATIVE_VLAN_MISMATCH

Possible Issues:
 - Incorrect traffic forwarding
 - Security risks (VLAN hopping)
 - Unstable network behavior

**Troubleshooting**
Check trunk configuration:
```bash
show interfaces trunk
```
Found native VLAN mismatch warnings. To fix the issue, make native VLAN same on both switches.
Switch1:
```bash
conf t
int fa0/24
switchport trunk native vlan 99
end
write memory
```
<img width="546" height="203" alt="6 6" src="https://github.com/user-attachments/assets/714ab8b9-6d60-4b9f-b0ed-b50d8aeb6bd2" />

**Verification:**
```bash
show interfaces trunk
```
 - Native VLAN matches on both sides
 - No warning messages
 - Stable network

**7. Configure a management VLAN and assign an IP address for remote access. Test SSH or Telnet access to the switch.**

Topology:
- 2 × Switches (2950)
- 4 × User PCs (VLAN 10 & 20)
- 1 × Admin PC (VLAN 99)
- Trunk link between switches

<img width="815" height="442" alt="7_admin" src="https://github.com/user-attachments/assets/c0ccc058-a5e5-4c19-8a9d-325e33bd982a" />

**IP Addressing:**
VLAN 10:
- PC0 → 192.168.10.2
- PC1 → 192.168.10.3
VLAN 20:
- PC2 → 192.168.20.2
- PC3 → 192.168.20.3
VLAN 99 (Management):
- Switch0 → 192.168.99.1
- Switch1 → 192.168.99.2
- Admin PC → 192.168.99.10

**Create Management VLAN:**
```bash
enable
conf t
vlan 99
name MANAGEMENT
```
**Assign IP to Switch (SVI)**
Switch0:
```bash
interface vlan 99
ip address 192.168.99.1 255.255.255.0
no shutdown
```
Switch1:
```bash
interface vlan 99
ip address 192.168.99.2 255.255.255.0
no shutdown
```
**Assign Port to VLAN 99 (Admin PC):**
```bash
interface fa0/3
switchport mode access
switchport access vlan 99
no shutdown
```
**Configure Default Gateway:**
```bash
ip default-gateway 192.168.99.1
```
**Remote Access Configuration:**

### Telnet
```bash
line vty 0 4
password cisco
login
transport input telnet ssh
```

### SSH
```bash
hostname Switch0
ip domain-name lab.local
username admin password admin123
crypto key generate rsa
- Enter: 1024 (size)
ip ssh version 2
line vty 0 4
login local
transport input ssh
```

**Admin PC Testing:**

**Telnet**
```bash
telnet 192.168.99.1
```
<img width="411" height="161" alt="7_telnet" src="https://github.com/user-attachments/assets/15785f61-8fcb-4d77-903d-19440c4175d7" />

**SSH**
```bash
ssh -l admin 192.168.99.1
```
<img width="242" height="112" alt="7_ssh" src="https://github.com/user-attachments/assets/a24233f9-21d3-44a7-8050-1eec7919ef69" />

**Issue Faced:**
- Telnet worked correctly
- SSH showed: Connection closed by foreign host

Troubleshooting:
- Checked VLAN and IP configuration
- Verified connectivity using ping
- Checked SSH settings and Found incomplete configuration
- Reconfigured SSH properly:
  - Set hostname and domain name
  - Created username and password
  - Generated RSA keys
  - Enabled SSH version 2
  - Configured VTY lines with `login local`
  - Allowed only SSH access

<img width="417" height="237" alt="7_troubleshoot" src="https://github.com/user-attachments/assets/29e4545a-d732-4aaf-9372-8dd17e67632f" />

Final observation:
- Telnet working
- SSH working successfully
- Remote access to switch achieved

Which is better, telnet or ssh? => SSH (It encrypts all transmitted data for ensuring confidentiality and integrity over insecure networks)

**8. You have a Cisco switch and a VoIP phone that needs to be placed in a voice VLAN (VLAN 20). The data for the PC should remain in a separate VLAN (VLAN 10). Configure the switch port to support both voice and data traffic.**

**Topology:**
- 1 × Switch (2960)
- 1 × IP Phone
- 1 × PC
- 
<img width="520" height="127" alt="8_topo" src="https://github.com/user-attachments/assets/d832387b-614a-40a6-8546-9769cd98215c" />

According to the given scenario:
| VLAN | Purpose |
|------|--------|
| VLAN 10 | Data (PC) |
| VLAN 20 | Voice (IP Phone) |

**Configuration Steps:**

Create VLANs:
```bash
enable
conf t

vlan 10
name DATA

vlan 20
name VOICE
```

Configure Switch Port:
```bash
int fa0/1
switchport mode access
switchport access vlan 10
switchport voice vlan 20
no shutdown
```

PC Configuration:
IP Address: 192.168.10.2
Subnet Mask: 255.255.255.0

- IP Phone separates traffic internally:
  - Voice traffic → VLAN 20
  - Data traffic → VLAN 10
- Single port carries both types of traffic

**Verification:**
Performed the following in Switch CLI:
```bash
show vlan brief
```
<img width="683" height="382" alt="8_switch" src="https://github.com/user-attachments/assets/c544144c-3814-43f9-865f-5a197acd53fc" />

Both DATA and VOICE vlan are configured

```bash
show interfaces fa0/1 switchport
```
<img width="457" height="387" alt="8_switchport" src="https://github.com/user-attachments/assets/61673eda-3030-4b88-9c2a-b20578a05f92" />

Checked and verified the configured ports and trunk port.

```bash
show cdp neighbors
```
<img width="608" height="97" alt="8_cdp" src="https://github.com/user-attachments/assets/f671e167-7c12-498f-8d9a-4e8ab46474d4" />

Checked the connected devices and found IP Phone in the list, hence successfully connected.

**9. You configured VLANs 10 and 20 on your switch and assigned ports to each VLAN. However, devices in VLAN 10 cannot communicate with devices in VLAN 20. Troubleshoot the issue.**

**Topology:**
- 1 × Switch (2960)
- 1 × Router
- 4 × PCs

<img width="581" height="433" alt="9_topo" src="https://github.com/user-attachments/assets/57c7d85f-4b39-4d17-b228-591168a7fc8a" />

| VLAN | Devices | Network |
|------|--------|--------|
| VLAN 10 | PC0, PC1 | 10.0.0.0/24 |
| VLAN 20 | PC2, PC3 | 20.0.0.0/24 |

**IP Addressing:**

VLAN 10:
- PC0 → 10.0.0.2
- PC1 → 10.0.0.3
- Gateway → 10.0.0.1

VLAN 20:
- PC2 → 20.0.0.2
- PC3 → 20.0.0.3
- Gateway → 20.0.0.1

Devices in VLAN 10 are unable to communicate with devices in VLAN 20.

**VLAN Configuration in Switch:**
Create VLANs
```bash
enable
conf t

vlan 10
exit

vlan 20
exit

int range fa0/1-2
switchport mode access
switchport access vlan 10

int range fa0/3-4
switchport mode access
switchport access vlan 20

interface fa0/24
switchport mode trunk
```

**Ping test between VLAN 10 and VLAN 20:**
<img width="472" height="208" alt="9_ping_fail" src="https://github.com/user-attachments/assets/40e07776-ae93-4d30-afa1-1b7b436a53af" />
The ping test between different VLANs fails.

**Troubleshooting:**
Verify VLAN Configuration:
```bash
show vlan brief
```
<img width="626" height="507" alt="9_vlan" src="https://github.com/user-attachments/assets/efb5e97f-c6fe-46c5-82e6-91a4338cdce1" />

Ports correctly assigned to VLAN 10 and VLAN 20

Different VLANs cannot communicate with each other without a layer-3 device.
 So, the solution is: **Router-on-a-Stick**

 Adding a Router to the topology:
 <img width="645" height="603" alt="9_topo_router" src="https://github.com/user-attachments/assets/b5962353-966c-4e57-a2f2-c77664241c7e" />

**Router Configuration**
Subinterface for VLAN 10:
```bash
interface fa0/0.10
encapsulation dot1Q 10
ip address 10.0.0.1 255.255.255.0
```
Subinterface for VLAN 20:
```bash
interface fa0/0.20
encapsulation dot1Q 20
ip address 20.0.0.1 255.255.255.0
```
Enable the interface:
```bash
int fa0/0
no shutdown
```
Check if the subnets are configured correctly:
```bash
show ip route
```
<img width="583" height="262" alt="9_subnet" src="https://github.com/user-attachments/assets/84cd7957-26ec-4a70-aabb-30ad1aa608c3" />

**Testing using ping:**
<img width="628" height="472" alt="9_ping" src="https://github.com/user-attachments/assets/924ae329-d1bb-4813-9f04-13f9efbee9eb" />

Successful ping demonstrates that the issue has been troubleshooted.

---

**10. Try Inter VLAN routing with Router**

**Topology:**
- 1 × Router (2811)
- 2 × Switches (2960)
- 4 × PCs

<img width="717" height="537" alt="10_topo" src="https://github.com/user-attachments/assets/3200ffd5-740e-4419-a298-6b220d6cb739" />

| VLAN | Department | Network |
|------|-----------|--------|
| VLAN 10 | IT | 192.168.10.0/24 |
| VLAN 20 | HR | 192.168.20.0/24 |

IP Addressing:
VLAN 10 (Switch0):
- PC0 → 192.168.10.2  
- PC1 → 192.168.10.3  
- Gateway → 192.168.10.1  
VLAN 20 (Switch1):
- PC2 → 192.168.20.2  
- PC3 → 192.168.20.3  
- Gateway → 192.168.20.1  

**Switch Configuration:**
Switch0 (VLAN 10):
```bash
enable
configure terminal

vlan 10
name IT

interface range fa0/1-2
switchport mode access
switchport access vlan 10

interface fa0/24
switchport mode access
switchport access vlan 10
```
Switch1 (VLAN 20):
```bash
enable
configure terminal

vlan 20
name HR

interface range fa0/1-2
switchport mode access
switchport access vlan 20

interface fa0/24
switchport mode access
switchport access vlan 20
```

**Router Configuration:**
```bash
enable
configure terminal

interface fa0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit

interface g0/1
ip address 192.168.20.1 255.255.255.0
no shutdown
exit
```

**Testing**:

Ping within VLAN:
<img width="632" height="572" alt="10_ping_intra_vlan" src="https://github.com/user-attachments/assets/4193baf9-baf8-406f-b3b7-3ebf81188aa8" />

Ping between different VLAN:
<img width="632" height="645" alt="10_ping_inter_vlan" src="https://github.com/user-attachments/assets/03c39582-ef2c-44c6-bd5e-80e6d87f580e" />

All the pings are successful, hence Inter-VLAN routing is done successfully with a router.

---

**11. Implement ACLs to restrict traffic based on source and destination ports.Test rules by simulating legitimate and unauthorized traffic.**

**Topology:**
The network consists of:
 - 2 PCs (PC0, PC1)
 - 1 Switch
 - 1 Router (2911)
 - 1 Server

<img width="626" height="272" alt="11_topo" src="https://github.com/user-attachments/assets/bd30bb60-20b9-4296-b63b-26a9b77ddeb1" />

**IP Addressing:**
| Device            | IP Address     | Subnet Mask     | Gateway       |
|------------------|---------------|-----------------|--------------|
| PC0              | 192.168.1.2   | 255.255.255.0   | 192.168.1.1  |
| PC1              | 192.168.1.3   | 255.255.255.0   | 192.168.1.1  |
| Router (g0/0)    | 192.168.1.1   | 255.255.255.0   | —            |
| Router (g0/1)    | 192.168.2.1   | 255.255.255.0   | —            |
| Server           | 192.168.2.100 | 255.255.255.0   | 192.168.2.1  |

**Router Configuration:**
```bash
enable
configure terminal

interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface g0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
```

**Server Configuration:**
HTTP service: ON
FTP service: ON

**Testing Before ACL:**

From PC:
 - Ping to server is Successful
 - HTTP access is Successful
 - FTP access is Successful

<img width="637" height="567" alt="11_before_acl_ftp" src="https://github.com/user-attachments/assets/34bba655-2cf3-49f0-9bd1-0443aebac133" />

<img width="628" height="567" alt="11_before_acl_http" src="https://github.com/user-attachments/assets/d86ad300-37bd-4759-8eec-0517705a819a" />

**ACL Configuration portwise**
 - To allow legitimate HTTP traffic (port 80)
 - To block unauthorized FTP traffic (port 21)
```bash
access-list 101 permit tcp any host 192.168.2.100 eq 80
access-list 101 deny tcp any host 192.168.2.100 eq 21
access-list 101 permit ip any any

interface g0/0
ip access-group 101 in
```

Access Lists Command:
| Part | Meaning |
|------|--------|
| `access-list` | Command used to create an ACL rule |
| `101` | ACL number (100–199 for Extended ACL) |
| `permit` | Action to allow traffic (`deny` would block) |
| `tcp` | Protocol (TCP used for HTTP, FTP, etc.) |
| `any` | Source IP address (any device) |
| `host 192.168.2.100` | Destination IP (specific server) |
| `eq 80` | Port number (80 = HTTP) |

**Testing After ACL:**
HTTP (Port 80)	is Allowed<br>
<img width="632" height="565" alt="11_after_acl_http" src="https://github.com/user-attachments/assets/881e70a3-3e5a-407b-9773-cbc6a6dbed9b" />

FTP (Port 21) is	Blocked <br>
<img width="380" height="223" alt="11_after_acl_ftp" src="https://github.com/user-attachments/assets/998d82f0-5ad5-4174-8752-a263d50aa26e" />

Ping is	Allowed<br>
<img width="457" height="221" alt="11_after_acl_ping" src="https://github.com/user-attachments/assets/729e351b-98b3-4cce-b2c9-f73e3b3c236c" />

**Verification:**
```bash
show access-lists
```
<img width="497" height="111" alt="11_acl" src="https://github.com/user-attachments/assets/61869880-6fd9-4d3c-a960-f981dc2e0439" />

Observed increasing match counters for rules
Confirmed ACL is actively filtering traffic

 Thus, ACL allows us to:
 - Allow legitimate web traffic (HTTP)
 - Block unauthorized FTP access
 - Demonstrate traffic filtering based on port numbers

**12. Configure a standard Access Control List (ACL) on a router to permit traffic from a specific IP range. Test connectivity to verify the ACL is working as intended.**

**Topology:**
 - 4 PCs
 - 1 Switch
 - 1 Router 
 - 1 Server

<img width="785" height="470" alt="12_TOPO" src="https://github.com/user-attachments/assets/6f782081-2de1-4793-862c-c3440c31ace7" />

**IP Addressing:**

| Device       | IP Address     | Subnet Mask     | Gateway       |
|--------------|---------------|----------------|--------------|
| PC-IT1       | 192.168.1.10  | 255.255.255.0  | 192.168.1.1  |
| PC-IT2       | 192.168.1.20  | 255.255.255.0  | 192.168.1.1  |
| PC-HR1       | 192.168.1.30  | 255.255.255.0  | 192.168.1.1  |
| PC-HR2       | 192.168.1.40  | 255.255.255.0  | 192.168.1.1  |
| Router g0/0 | 192.168.1.1   | 255.255.255.0  | —            |
| Router g0/1 | 192.168.2.1   | 255.255.255.0  | —            |
| Server       | 192.168.2.100 | 255.255.255.0  | 192.168.2.1  |

Two different departments are considered:
1) IT department : IP ranges from 192.168.1.10 to 192.168.1.29
2) HR department : IP ranges from 192.168.1.30 to 192.168.1.49

**Test before ACL:**
Both the departments can access the server:<br>
<img width="638" height="570" alt="12_before_acl_it_http" src="https://github.com/user-attachments/assets/8af661d4-596c-40d8-9b82-bb54778ce160" />

<img width="635" height="577" alt="12_before_acl_hr_http" src="https://github.com/user-attachments/assets/b4fc4980-37fc-4adf-ba12-202e35ecd30f" />

**Static ACL configuration:**
The goal is to permit only IT department PCs (192.168.1.10–192.168.1.29) to access the server and deny HR department PCs (192.168.1.30–192.168.1.49).

Challenge:
Standard ACLs work with wildcard masks, which only match power-of-2 blocks.
The IT IP range (10–29) is not a single power-of-2 block, so it must be split into three separate blocks to match exactly without permitting extra IPs.

**ACL Configuration:**
```bash
access-list 1 permit 192.168.1.10 0.0.0.5   # permits 10–15
access-list 1 permit 192.168.1.16 0.0.0.7   # permits 16–23
access-list 1 permit 192.168.1.24 0.0.0.5   # permits 24–29

interface g0/0
ip access-group 1 in
```

**Testing After ACL:**

Ping is allowed only from IT IPs (10–29) and fails from blocked HR IPs (30–49).

<img width="631" height="565" alt="12_after_acl_ping_hr" src="https://github.com/user-attachments/assets/f62e2343-d966-4d3c-a1af-ae85190d2900" />
<BR>
Destination host is unreachable for HR PCs.
<img width="632" height="572" alt="12_after_acl_http" src="https://github.com/user-attachments/assets/abf6173a-2b2e-4d4b-bd8a-41a3f13ed773" />
<BR>
Request timed out to access HTTP server for HR PCs.

Thus, standard ACL is configured and verified. <BR>

- 
**13. Create an extended ACL to block specific applications, such as HTTP or FTP traffic.Test the ACL rules by attempting to access blocked services.**
  
**Topology:**
 - IT Department PCs: 192.168.2.10 – 192.168.2.29
 - HR Department PCs: 192.168.2.30 – 192.168.2.49
 - Server: 192.168.2.100
 - Router: 2911
 - Switch: 2960-24TT
<img width="747" height="470" alt="13_topo" src="https://github.com/user-attachments/assets/7d284554-0e12-42bb-b6b2-30c992577753" />
Topology same as standard ACL setup.

To configure extended ACL, the following conditions are determined:
 - Allow HTTP (port 80) access only from IT PCs to the server.
 - Allow FTP (port 21) access only from HR PCs to the server.
 - Deny the opposite traffic.
 - Permit all other traffic.

**Extended ACL Configuration:**
```bash
enable
conf t
access-list 110 permit tcp 192.168.2.10 0.0.0.19 host 192.168.2.100 eq 80
access-list 110 deny tcp 192.168.2.10 0.0.0.19 host 192.168.2.100 eq 21
access-list 110 permit tcp 192.168.2.30 0.0.0.19 host 192.168.2.100 eq 21
access-list 110 deny tcp 192.168.2.10 0.0.0.19 host 192.168.2.100 eq 80
access-list 110 permit ip any any

int g0/0
ip access-group 110 in
exit
write memory
```

0.0.0.19 is the wildcard mask for 20 IP addresses in each department range. Extended ACLs allow filtering by protocol (TCP/UDP), port number, and source as well as destination IP.

**Testing:**
IT dept can access HTTP service:<BR>
<img width="633" height="567" alt="13_it_http" src="https://github.com/user-attachments/assets/5a524639-9692-4c81-a37c-b8b54eb20d5b" />
<BR>
IT dept cannot access FTP service:<BR>
<img width="637" height="482" alt="13_it_ftp" src="https://github.com/user-attachments/assets/a7e51387-4555-4887-ac24-46471239b743" />
<BR>
HR dept can access FTP service:<BR>
<img width="637" height="570" alt="13_hr_ftp" src="https://github.com/user-attachments/assets/5fcd32be-b2aa-421e-8221-7c39b035d74f" />
<BR>
HR dept cannot access HTTP service:<BR>
<img width="637" height="566" alt="13_hr_http" src="https://github.com/user-attachments/assets/e5def095-2bba-44ce-8a79-03a7ab3ce9bb" />
<BR>
Hence, the ACL rules are tested and verified.

**14. Try Static NAT, Dynamic NAT and PAT to translate IPs**

**Topology:**
- 1 Router
- 1 Switch
- 2 PCs (Internal Network)
- 1 Server (External Network)

<img width="675" height="272" alt="14_topo" src="https://github.com/user-attachments/assets/2fd1e5e5-32da-4344-bc36-e34625719223" />

**IP Addressing:**
| Device | Interface        | IP Address     | Subnet Mask     |
|--------|-----------------|----------------|-----------------|
| Router | Gig0/0 (Inside)  | 192.168.1.1    | 255.255.255.0   |
| Router | Gig0/1 (Outside) | 200.0.0.1      | 255.255.255.0   |
| PC0    | -               | 192.168.1.2   | 255.255.255.0   |
| PC1    | -               | 192.168.1.3   | 255.255.255.0   |
| Server | -               | 200.0.0.2      | 255.255.255.0   |

To configure and verify:
- Static NAT (One-to-One Mapping)
- Dynamic NAT (Pool-Based Mapping)
- PAT (Overloading)

**Static NAT Configuration:**
```bash
enable
conf t

ip nat inside source static 192.168.1.2 200.0.0.2

int g0/0
ip nat inside
exit

int g0/1
ip nat outside
exit

end
write memory
```

**Verify:**
```bash
show ip nat translations
```

<img width="616" height="116" alt="14_static" src="https://github.com/user-attachments/assets/f8367c55-9ebc-4818-b4f6-5a8018de8bcc" />

 - Maps one private IP to one public IP permanently
 - Used for servers that need external access

**Dynamic NAT Configuration:**
```bash
enable
conf t

access-list 1 permit 192.168.1.0 0.0.0.255
ip nat pool POOL1 200.0.0.3 200.0.0.5 netmask 255.255.255.0
ip nat inside source list 1 pool POOL1

int g0/0
ip nat inside
exit

int g0/1
ip nat outside
exit

end
write memory
```

**Check:**
```bash
show ip nat translations
```

<img width="617" height="113" alt="14_dynamic" src="https://github.com/user-attachments/assets/ce3f532f-b9f8-4a6b-a149-c49a3b5ed104" />

 - Uses a pool of public IPs
 - Each device gets a temporary public IP
 - Limited by pool size

**PAT (Port Address Translation):**
```bash
enable
conf t

access-list 1 permit 192.168.1.0 0.0.0.255
ip nat inside source list 1 interface FastEthernet0/1 overload

int g0/0
ip nat inside
exit

int g0/1
ip nat outside
exit

end
write memory
```

**Check:**
```bash
show ip nat translations
```

<img width="617" height="117" alt="14_pat" src="https://github.com/user-attachments/assets/34d5e957-9949-4387-a497-0a7150304f80" />

 - Multiple devices share one public IP
 - Differentiation done using port numbers
 - Most commonly used for internet access
 - 
**Testing:**
Ping external server from PCs

<img width="632" height="672" alt="14_ping" src="https://github.com/user-attachments/assets/c00a4676-e220-4b19-bcb5-67cf2f456250" />

**Differences Between NAT Types:**

| Feature               | Static NAT     | Dynamic NAT    | PAT              |
|----------------------|---------------|----------------|------------------|
| Mapping              | One-to-One     | One-to-Pool    | Many-to-One      |
| Public IP Requirement| High           | Medium         | Low              |
| Port Usage           | No             | No             | Yes              |
| Use Case             | Hosting servers| Limited users  | Internet access  |

Successfully configured and verified Static NAT, Dynamic NAT and PAT.

**15. Download iperf in laptop/phone and make sure they are in same network. Try different iperf commands with tcp, udp, birectional, reverse, multicast, parallel options and analyze the bandwidth and rate of transmission, delay, jitter etc.**

**Requirements:**
- Laptop (iPerf3 installed)
- Mobile phone with iPerf app
- Same WiFi network connection

- Both laptop and mobile phone were connected to the same wireless network.
- The laptop was configured as the iPerf server.
- The phone/laptop acted as the client.

Found the IP address of the laptop using:
```bash
ipconfig
```
<img width="947" height="792" alt="15_ipconfig" src="https://github.com/user-attachments/assets/1fc0ab5d-937f-4c79-9d62-f943855bb882" />

Started the iPerf server:
```bash
iperf3 -s
```
<img width="1136" height="582" alt="15_initialize" src="https://github.com/user-attachments/assets/a129417d-9a16-4d78-b815-30d1455606e5" />

Executed different iPerf commands from client side and analyzed the output metrics.
**iPerf Commands Used:**
TCP Test:
```bash
iperf3 -c 192.168.1.6
```
<img width="1352" height="492" alt="15_tcp" src="https://github.com/user-attachments/assets/62a93b1c-342b-443a-a05d-0429cba369d9" />

UDP Test:
```bash
iperf3 -c 192.168.1.6 -u -b 10M
```
<img width="1282" height="435" alt="15_udp" src="https://github.com/user-attachments/assets/0249b8c3-33a0-4164-bed5-2a0e5d1c7607" />

Reverse Mode:
```bash
iperf3 -c 192.168.1.6 -R
```
<img width="1310" height="525" alt="15_reverse" src="https://github.com/user-attachments/assets/fc7d4fbe-6bf8-4d12-92bc-30794fa3cdbe" />

Bidirectional Test:
```bash
iperf3 -c 192.168.1.6
iperf3 -c 192.168.1.6 -R
```
<img width="1027" height="912" alt="15_bidir" src="https://github.com/user-attachments/assets/fe23d6a8-6187-4b5d-b329-4e9de359d683" />

Since the --bidir option was not supported in the installed version of iPerf, bidirectional communication was analyzed by performing both forward (client-to-server) and reverse (server-to-client) tests separately.

Parallel Streams:
```bash
iperf3 -c 192.168.1.X -P 5
```
<img width="1087" height="817" alt="15_parallel_1" src="https://github.com/user-attachments/assets/2b930410-ccbd-4ecb-ae14-a71d892f14d2" />
<img width="742" height="970" alt="15_parallel_2" src="https://github.com/user-attachments/assets/21987885-e9ee-4276-b99b-e677daef459d" />

Multicast Test:
```bash
iperf3 -c 224.1.1.1 -u -b 5M
```
However, the following error was encountered: "unable to connect to server: Cannot assign requested address"

This indicates that the local network environment does not support multicast communication. This limitation is commonly observed in WiFi networks and standard system configurations where multicast routing (IGMP) is not enabled. Hence, multicast testing could not be successfully performed in this setup.

![WhatsApp Image 2026-03-24 at 15 43 26 (1)](https://github.com/user-attachments/assets/9dbbc88c-a4d9-49a2-a395-dd44201cdc00)
![WhatsApp Image 2026-03-24 at 15 43 26 (2)](https://github.com/user-attachments/assets/222ac8f4-4a4a-4fc7-b0d8-cd47368a1b46)
![WhatsApp Image 2026-03-24 at 15 43 26](https://github.com/user-attachments/assets/6c9baed8-26ad-41b0-a986-d0e20551f50f)

**Parameters Observed:**

| Parameter        | Description                              |
|-----------------|------------------------------------------|
| Bandwidth       | Data transfer rate (Mbps)                |
| Transfer        | Total data transmitted                   |
| Jitter          | Variation in packet delay (UDP)          |
| Packet Loss     | Number of lost packets                   |
| Retransmissions | TCP packet re-sending                    |
| Delay           | Time taken for packet transmission       |

**Observations:**
 - TCP provided reliable communication with retransmissions when needed
 - UDP showed packet loss and jitter, useful for real-time applications
 - Reverse mode showed variation in upload and download speeds
 - Parallel streams increased bandwidth utilization
 - Multicast enabled communication with multiple receivers
 - Bidirectional testing showed network behavior in both directions
   
**Comparative Analysis:**

| Test Type     | Protocol | Key Metrics Observed        | Performance Insight              |
|---------------|----------|-----------------------------|---------------------------------|
| TCP           | TCP      | Bandwidth, Retransmissions  | Reliable but slightly slower    |
| UDP           | UDP      | Jitter, Packet Loss         | Faster but less reliable        |
| Reverse       | TCP      | Download Speed              | Shows asymmetry in network      |
| Bidirectional | TCP      | Upload & Download           | Network load handling           |
| Parallel      | TCP      | Bandwidth Increase          | Better utilization of network   |
| Multicast     | UDP      | Group Transmission          | Efficient for multiple clients  |

Successfully analyzed network performance using iPerf by executing various commands and observed key parameters such as bandwidth, jitter, delay, and packet loss under different conditions.
