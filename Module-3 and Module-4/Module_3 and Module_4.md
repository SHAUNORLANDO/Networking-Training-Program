**Networking Training program**
**Module 3 and 4 assessment questions**

Tools you can use for below questions: VirtualBox with Linux VMs, GNS3, Cisco Packet Tracer, Wireshark etc. <br>

**Simulate a small network with switches and multiple devices. Use ping to generate traffic and observe the MAC address table of the switch. Capture packets using Wireshark to analyze Ethernet frames and MAC addressing.**

A small LAN network was simulated using Cisco Packet Tracer consisting of one switch and three PCs. Each PC was configured with IP addresses in the same subnet. Connectivity between the devices was verified using the ping command. <br>
<img width="296" height="292" alt="1" src="https://github.com/user-attachments/assets/bc78ea0b-beca-4408-9de1-943d71c1f6ec" /> 
<br>
When ping traffic was generated, the switch dynamically learned the MAC addresses of the connected devices and stored them in its MAC address table. This table maps MAC addresses to specific switch ports. <br>
<img width="597" height="458" alt="2" src="https://github.com/user-attachments/assets/f771d46f-4bb3-4866-b44c-8d9843f14238" />
<br>
<img width="632" height="566" alt="3" src="https://github.com/user-attachments/assets/71099eaa-14ac-43f0-b2c0-68c88d48734a" />
<br>
Wireshark was used to capture network packets and analyze Ethernet frames. The captured frames showed the destination MAC address, source MAC address, EtherType field indicating the protocol, payload containing the data, and the frame check sequence used for error detection. <br>
<img width="1918" height="1017" alt="4" src="https://github.com/user-attachments/assets/e09d3c23-bce5-4168-ac2c-01844b3e8bf4" />
<br>

**Capture and analyze Ethernet frames using Wireshark. Inspect the structure of the frame, including destination and source MAC addresses, Ethertype, payload, and FCS. Use GNS3 or Packet Tracer to simulate network traffic.**

Cisco Packet Tracer was used to simulate network traffic:<br>
<img width="273" height="280" alt="5" src="https://github.com/user-attachments/assets/14114dc8-abbf-4f03-acb6-399d8b74cfd4" />
<br>
<img width="592" height="453" alt="6" src="https://github.com/user-attachments/assets/d63bddb6-5695-40f2-ba93-a731676988df" />
<br>
Ethernet frames were captured using Wireshark and analyzed to understand their structure. <br>
The Ethernet frame consists of several important fields:
 - Destination MAC address: identifies the receiving device
 - Source MAC address: identifies the transmitting device.
 - EtherType field: specifies the protocol encapsulated in the payload, such as IPv4, ARP, or IPv6.
 - Payload: contains the actual data being transmitted, which may include IP packets, TCP segments, or application data.
 - Frame Check Sequence (FCS): used for error detection to ensure that the frame was transmitted without corruption.
<br>
Wireshark was used to inspect these fields and analyze how data is transmitted at the Ethernet layer. <br>
<img width="1918" height="1017" alt="7" src="https://github.com/user-attachments/assets/74ca9738-6e2a-4bf6-8439-32a73ece747a" />
<br>

**Configure static IP addresses, modify MAC addresses, and verify network connectivity using ping and ifconfig commands.**

The ifconfig command was used to display the current configuration of the network interface. The interface enp0s3 was identified with an IP address in the local network. <br>

Command:
```bash
ifconfig
```
Output: <br>
<img width="686" height="332" alt="8" src="https://github.com/user-attachments/assets/3043d779-9366-4fb8-b80e-a334fe4c945a" />
<br>
A static IP address was configured using the ifconfig command.
```bash
sudo ifconfig enp0s3 192.168.1.100 netmask 255.255.255.0
```
The MAC address of the network interface was then modified using the hw ether option.
```bash
sudo ifconfig enp0s3 down
sudo ifconfig enp0s3 hw ether 00:11:22:33:44:55
sudo ifconfig enp0s3 up
```
Output:<br>
<img width="683" height="327" alt="9" src="https://github.com/user-attachments/assets/b4d30e7b-bc7c-4e81-8074-ca260d105f99" />
<br>
After modifying the MAC address, the ping command returned "Destination Host Unreachable". This occurred because the network router did not recognize the modified MAC address.<br>
<img width="703" height="177" alt="10" src="https://github.com/user-attachments/assets/f5100a6c-d495-4df5-93c6-354c2d5ec42f" />
<br>
The issue was resolved by restoring the original MAC address of the interface. After restoring the original MAC address, the ping command successfully verified network connectivity. <br>
<img width="646" height="232" alt="11" src="https://github.com/user-attachments/assets/96a51cc4-d3fe-401c-8358-3383f6708c1d" />
<br>

**Troubleshoot Ethernet Communication with ping and traceroute -> Using cisco packet tracer:**
**Create a simple LAN setup with two Linux machines connected via a switch.** <br>
<img width="490" height="142" alt="12" src="https://github.com/user-attachments/assets/9727c999-09d5-411d-a55c-3e46cb3f3b34" />
<br>
**Ping from one machine to the other. If it fails, use ifconfig to ensure the IP addresses are configured correctly.** <br>
<img width="632" height="567" alt="13" src="https://github.com/user-attachments/assets/ac30db81-8e6d-4bbd-ae17-b9a2151d15f6" />
<br>
**Use traceroute to identify where the packets are being dropped if the ping fails.** <br>
<img width="465" height="117" alt="14" src="https://github.com/user-attachments/assets/a6ff0daa-0a95-4d9e-9f1d-08da4332ac15" />
<br>
**Research the Linux kernel's handling of Ethernet devices and network interfaces. Write a short report on how the Linux kernel supports Ethernet communication (referencing kernel.org documentation).**
 - The Linux kernel provides support for Ethernet communication through its networking subsystem. Network interfaces such as Ethernet adapters are managed by device drivers within the kernel. Each Ethernet device is represented as a network interface (for example, eth0 or enp0s3).
 - The kernel networking stack processes packets through multiple layers including the network device driver, link layer (Ethernet), network layer (IP), and transport layer (TCP/UDP). When a packet is transmitted, the kernel encapsulates the data into an Ethernet frame containing source and destination MAC addresses.
 - The kernel also manages routing tables, ARP resolution, and packet forwarding. Commands such as ip, ifconfig, and route interact with the kernel to configure and manage network interfaces.
 - Linux also supports bridging and switching functionality through the bridge subsystem, which allows the system to act like a network switch by maintaining a forwarding database (FDB) mapping MAC addresses to ports.
<br>
Reference:
https://www.kernel.org/doc/html/latest/networking/
<br>

**Describe how you would configure a basic LAN interface using the ip command in Linux
(kernel.org).** <br>
Commands:
```bash
ip addr show
sudo ip addr add 192.168.1.50/24 dev enp0s3
sudo ip link set enp0s3 up
ip addr show
```
Execution:<br>
<img width="928" height="542" alt="15" src="https://github.com/user-attachments/assets/d064a6cd-b4ad-4c49-a79c-46a817aebfa9" />
<br>
**Use Linux to view the MAC address table of a switch (if using a Linux-based network switch).** <br>
Commands:
```bash
bridge fdb show
ip link
```
<br>
<img width="1032" height="200" alt="16" src="https://github.com/user-attachments/assets/45f49804-c462-45df-a94b-3eb8b6a73189" />
 
**Use the bridge or ip link commands to inspect the MAC table and demonstrate a basic switch's operation.** <br>
Commands: <br>
Inspecting neigbour ARP table:
```bash
ip neigh
```
Generating network traffic:
```bash
ping 192.168.1.1
```
Inspecting MAC table:
```bash
bridge fdb show
```
<br>
<img width="683" height="435" alt="17" src="https://github.com/user-attachments/assets/02c7f86f-6f2e-428b-8916-06979f61df34" />

