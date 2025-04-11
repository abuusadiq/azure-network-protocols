<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04


<h2>Actions and Observations</h2>

First i will be creating two virtual machines in the same resource group and the same virtual network, the First one with Windows 10 and 2nd with Ubuntu 22-24. (For this lab purpose, we can change authentication to password for easy access.)

![image](https://github.com/user-attachments/assets/478951f3-f7c5-4138-902a-326f464799d6)

Next Step we can log into the Windows VM via remote desktop. and install wireshark in the windows vm to capture network protocols in action.

![image](https://github.com/user-attachments/assets/ed264da4-1adc-4007-b024-4340af18f126)

![image](https://github.com/user-attachments/assets/27b34fa4-66bd-4777-9c90-53e0e43afc88)





















