**Networking Training program**
**Module 1 and 2 assessment questions.**

1. Consider a case, a folder has multiple files and how would copy it to destination machine path (Try using SCP, cp options in Linux)

```bash
scp -r Module_1 shaun@192.168.1.9:/home/shaun/Networking_Assessments/Module_1_secure_copy
```

```bash
cp -r Module_1 Module_1_copy
```

2. Host a FTP and SFTP server and try PUT and GET operations.

**FTP**
```bash
ftp 192.168.1.9
```
```bash
ftp> put ftp.txt
```
```bash
local: ftp.txt remote: ftp.txt
229 Entering Extended Passive Mode (|||56679|)
150 Ok to send data.
100% |***********************************|     9      137.32 KiB/s    00:00 ETA
226 Transfer complete.
9 bytes sent in 00:00 (2.00 KiB/s)
```
```bash
ftp> get ftp.txt
```
```bash
local: ftp.txt remote: ftp.txt
229 Entering Extended Passive Mode (|||39109|)
150 Opening BINARY mode data connection for ftp.txt (9 bytes).
100% |***********************************|     9       65.10 KiB/s    00:00 ETA
226 Transfer complete.
9 bytes received in 00:00 (9.32 KiB/s)
```

***SFTP***
```bash
sftp shaun@192.168.1.9
```
```bash
sftp> put ftp.txt
```
```bash
Uploading ftp.txt to /home/shaun/ftp.txt
ftp.txt                                       100%    9     4.6KB/s   00:00
```
```bash
sftp> get ftp.txt
```
```bash
Fetching /home/shaun/ftp.txt to ftp.txt
ftp.txt                                       100%    9     1.8KB/s   00:00
```


3. Explore with Wireshark/TCP-dump/cisco packet tracer tools and learn about packets filters.

**WIRESHARK**
Packet Capture and Network Traffic Analysis

```bash
ping google.com
```
Filters used:
```bash
icmp
tcp
ftp
ip.addr == 192.168.1.9
```

**TCP-DUMP**
Packet capture
```bash
sudo tcpdump -i enp0s3
sudo tcpdump -i enp0s3 icmp
sudo tcpdump -i enp0s3 tcp
sudo tcpdump -i enp0s3 port 21
sudo tcpdump -i enp0s3 host 192.168.1.9
```
Save capture to file:
```bash
sudo tcpdump -i enp0s3 -w capture.pcap
```

**CISCO PACKET TRACER**
Worked with packet capture and analysis
<img width="277" height="177" alt="cisco packet tracer" src="https://github.com/user-attachments/assets/0995a774-80af-400d-93b6-6ea2c63b0280" />

4. Understand linux utility commands like - ping, arp (Understand each params from ifconfig output)
**PING**
Command:
```bash
ping google.com
```
Output:
```bash
PING google.com (142.250.77.110) 56(84) bytes of data.
64 bytes from pnmaaa-aq-in-f14.1e100.net (142.250.77.110): icmp_seq=1 ttl=118 time=3.88 ms
```
**ARP**
Command:
```bash
arp -a
```
Output:
```bash
arp -a
? (192.168.1.9) at d4:e9:8a:df:83:15 [ether] on enp0s3
_gateway (192.168.1.1) at 44:95:3b:98:11:d0 [ether] on enp0s3
```

**IFCONFIG**
Command:
```bash
ifconfig
```
Output:
```bash
enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.10  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fd17:625c:f037:2:ba43:5744:5313:bfb6  prefixlen 64  scopeid 0x0<global>
        inet6 fd17:625c:f037:2:e8b9:f501:c855:ba3e  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::c2eb:2675:5d0a:3e50  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:13:5a:3c  txqueuelen 1000  (Ethernet)
        RX packets 107161  bytes 153264839 (153.2 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15778  bytes 1221154 (1.2 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
5. Understand what happens when duplicate IPs configured in a network.
 
1. Network instability occurs.
2. Ping responses become inconsistent.
3. Packet loss may occur.
4. The ARP table keeps changing.
5. The system may display an "IP address conflict" warning.

6. Understand how to access remote system using (VNC viewer, Anydesk, teamviewer and remote desktop connections)

**Tools Studied:**
1. VNC Viewer
2. AnyDesk
3. TeamViewer
4. Remote Desktop Connection (RDP)

- Installed remote software on both systems.
- Obtained IP address or ID from remote machine.
- Entered IP/ID in client machine.
- Authenticated using password.
- Successfully accessed remote desktop interface.

7. How to check your default gateway is reachable or not and understand about default gateway.

To find default gateway:
```bash
ip route
```
Output:
```bash
default via 192.168.1.1 dev enp0s3 proto dhcp metric 100 
192.168.1.0/24 dev enp0s3 proto kernel scope link src 192.168.1.10 metric 100
```

To check if default gateway is reachable:
```bash
ping 192.168.1.1
```
Output:
```bash
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=4.56 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=2.63 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=6.88 ms
^C
--- 192.168.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2001ms
rtt min/avg/max/mdev = 2.629/4.691/6.882/1.738 ms
```

8. Check iwconfig/ifconfig to understand in detail about network interfaces (check about interface speed, MTU and other parameters)

**IFCONFIG**
Command:
```bash
ifconfig
```
Output:
```bash
enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.10  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fd17:625c:f037:2:ba43:5744:5313:bfb6  prefixlen 64  scopeid 0x0<global>
        inet6 fd17:625c:f037:2:e8b9:f501:c855:ba3e  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::c2eb:2675:5d0a:3e50  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:13:5a:3c  txqueuelen 1000  (Ethernet)
        RX packets 107161  bytes 153264839 (153.2 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15778  bytes 1221154 (1.2 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
**IWCONFIG**
Command:
```bash
iwconfig
```
Output:
```bash

```
To check speed:
```bash
sudo ethtool enp0s3
```
To check MTU:
```bash
ip link show
```

9. Log in to your home router's web interface (usually at 192.168.1.1 or 192.168.0.1) and check the connected devices list.
Checked default gateway using:
```bash
ip route
```
Found gateway IP as:
  ```bash
192.168.1.1
```
Opened web browser and entered:
```bash
http://192.168.1.1
```
Logged in using router admin credentials. Navigated to: Connected Devices / DHCP Clients List section.

10. Explain how a DHCP server assigns IP addresses to devices in your network.

DHCP server assigns IP addresses through DORA Process: 
1. Discover – Client broadcasts a request for IP address.
2. Offer – DHCP server offers an available IP address.
3. Request – Client requests the offered IP address.
4. Acknowledge – Server confirms and assigns the IP address.


11. Using a terminal, connect to a remote machine via SSH and telnet.

**SSH**
Commands:
```bash
sudo systemctl start ssh
sudo systemctl status ssh
ssh shaun@192.168.1.10
```

**TELNET**
Commands:
```bash
sudo systemctl start inetd
telnet 192.168.1.10
```
