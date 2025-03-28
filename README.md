<h1>NOTE: LAB IN PROGRESS! WILL BE DONE SOON!</h1>

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
This tutorial walks through creating Azure VMs, analyzing network traffic with Wireshark, and configuring firewall rules using Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps Overview </h2>

- Create Virtual Machines
- Observe ICMP Traffic
- Configure a Firewall (Network Security Group)
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
- Lab Cleanup

<h2>Installation and Actions</h2>

<h3 align="center"> Create Virtual Machines </h3>

<p align="center">
Create Resource Group
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Create Windows 10 Virtual Machine (VM)
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Create Linux (Ubuntu) Virtual Machine (VM)
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Ensure both VMs are in the same Virtual Network/Subnet
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<h3 align="center"> Observe ICMP Traffic </h3>

<p align="center">
Install Windows App then run the Windows 10 VM by using the public IP address from Azure.
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
In Windows 10 VM Install Wireshark
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Open Wireshark and start packet capture. Filter for ICMP traffic only
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Retrieve the private IP address of the Ubuntu VM (linux-vm) from Azure and attempt to ping it from within the Windows 10 VM. Then observe ping requests and replies within WireShark.
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
From Windows 10 VM attempt to ping a public website (ex: google.com)
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<h3 align="center"> Configuring a Firewall (Network Security Group) </h3>
<h4 align="center"> Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM.  </h3>

<p align="center">
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is.
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working). Then stop the ping activity.
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<h3 align="center">Observe DHCP Traffic</h3>

<p align="center">
Back in Wireshark, filter for DHCP traffic only.
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<h4 align="center">From your Windows 10 VM, attempt to issue your VM a new IP address from the command line</h4>

<p align="center">
Open PowerShell as admin and run: ipconfig /renew. Then observe the DHCP traffic appearing in WireShark.
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<h3 align="center">Observe DNS Traffic</h3>

<p align="center">
Back in Wireshark, filter for DNS traffic only.
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are. Then observe the DNS traffic slow being shown in WireShark.
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<h3 align="center">Observe RDP Traffic</h3>

<p align="center">
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389). Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
</p>
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p align="center">
Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted
</p>
<br/>
<br/>

<h3 align="center">Lab Cleanup</h3>

<p align="center">
(1) Close Remote Desktop connection (2) Delete the Resource Group(s) created at the beginning of this lab (3) Verify Resource Group Deletion. This is done in order to save money. If you do not delete your resources your account will keep getting charged!
<br/>
<p>
<img src="https://i.imgur.com/0NZNyOY.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p>In this lab, we learned essential networking and cloud skills, including setting up and managing Virtual Machines (VMs) in Microsoft Azure. We gained hands-on experience using Wireshark to capture and analyze network traffic for protocols like ICMP, SSH, DHCP, DNS, and RDP. Additionally, we practiced configuring firewall rules using Network Security Groups (NSGs) to control inbound traffic. These skills are crucial for cloud administration, network security, and troubleshooting network issues in real-world IT environments.
</p>

<br/>
<p>END OF TUTORIAL
</p>
