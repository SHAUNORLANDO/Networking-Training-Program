**Networking Training program**
**Module 3 and 4 assessment questions**

Tools you can use for below questions: VirtualBox with Linux VMs, GNS3, Cisco Packet Tracer, Wireshark etc.

Simulate a small network with switches and multiple devices. Use ping to generate traffic and observe the MAC address table of the switch. Capture packets using Wireshark to analyze Ethernet frames and MAC addressing.

A small LAN network was simulated using Cisco Packet Tracer consisting of one switch and three PCs. Each PC was configured with IP addresses in the same subnet. Connectivity between the devices was verified using the ping command.
<img width="296" height="292" alt="1" src="https://github.com/user-attachments/assets/bc78ea0b-beca-4408-9de1-943d71c1f6ec" />

When ping traffic was generated, the switch dynamically learned the MAC addresses of the connected devices and stored them in its MAC address table. This table maps MAC addresses to specific switch ports.
<img width="597" height="458" alt="2" src="https://github.com/user-attachments/assets/f771d46f-4bb3-4866-b44c-8d9843f14238" />

<img width="632" height="566" alt="3" src="https://github.com/user-attachments/assets/71099eaa-14ac-43f0-b2c0-68c88d48734a" />


Wireshark was used to capture network packets and analyze Ethernet frames. The captured frames showed the destination MAC address, source MAC address, EtherType field indicating the protocol, payload containing the data, and the frame check sequence used for error detection.
<img width="1918" height="1017" alt="4" src="https://github.com/user-attachments/assets/e09d3c23-bce5-4168-ac2c-01844b3e8bf4" />


Capture and analyze Ethernet frames using Wireshark. Inspect the structure of the frame, including destination and source MAC addresses, Ethertype, payload, and FCS. Use GNS3 or Packet Tracer to simulate network traffic.

Configure static IP addresses, modify MAC addresses, and verify network connectivityusing ping and ifconfig commands.

Troubleshoot Ethernet Communication with ping and traceroute -> Using cisco packet tracer:
Create a simple LAN setup with two Linux machines connected via a switch.

Ping from one machine to the other. If it fails, use ifconfig to ensure the IP addresses are configured correctly.
Use traceroute to identify where the packets are being dropped if the ping fails.
Research the Linux kernel's handling of Ethernet devices and network interfaces. Write a short report on how the Linux kernel supports Ethernet communication (referencing kernel.org documentation).
Describe how you would configure a basic LAN interface using the ip command in Linux
(kernel.org).
Use Linux to view the MAC address table of a switch (if using a Linux-based network switch).
Use the bridge or ip link commands to inspect the MAC table and demonstrate a basic switch's operation.
Submit your findings with explanations of what you observe.
