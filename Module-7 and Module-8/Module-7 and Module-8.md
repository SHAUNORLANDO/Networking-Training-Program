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
**6. Change the native VLAN on a trunk port.Test for VLAN mismatches and troubleshoot.**
**7. Configure a management VLAN and assign an IP address for remote access.Test SSH or Telnet access to the switch.**

8. You have a Cisco switch and a VoIP phone that needs to be placed in a voice VLAN (VLAN 20). The data for the PC should remain in a separate VLAN (VLAN 10). Configure the switch port to support both voice and data traffic.
9. You configured VLANs 10 and 20 on your switch and assigned ports to each VLAN. However, devices in VLAN 10 cannot communicate with devices in VLAN 20. Troubleshoot the issue.
10. Try Inter VLAN routing with Router
11. Implement ACLs to restrict traffic based on source and destination ports.Test rules by simulating legitimate and unauthorized traffic.
12. Configure a standard Access Control List (ACL) on a router to permit traffic from a specific IP range. Test connectivity to verify the ACL is working as intended.
13. Create an extended ACL to block specific applications, such as HTTP or FTP traffic.Test the ACL rules by attempting to access blocked services.
14. Try Static NAT, Dynamic NAT and PAT to translate IPs
15. Download iperf in laptop/phone and make sure they are in same network. Try different iperf commands with top, udp, birectional, reverse, multicast, parallel options and analyze the bandwidth and rate of transmission, delay, jitter etc.
