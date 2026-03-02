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


4. Understand linux utility commands like - ping, arp (Understand each params from ifconfig output)


5. Understand what happens when duplicate IPs configured in a network.


6. Understand how to access remote system using (VNC viewer, Anydesk, teamviewer and remote desktop connections)


7. How to check your default gateway is reachable or not and understand about default gateway.


8. Check iwconfig/ifconfig to understand in detail about network interfaces (check about interface speed, MTU and other parameters)


9. Log in to your home router's web interface (usually at 192.168.1.1 or 192.168.0.1) and check the connected devices list.


10. Explain how a DHCP server assigns IP addresses to devices in your network.


11. Using a terminal, connect to a remote machine via SSH and telnet.
