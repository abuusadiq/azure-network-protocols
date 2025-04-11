<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, RDP/RDH, DNS, HTTP/S)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04


<h2>Actions and Observations</h2>

First, I will be creating two virtual machines in the same resource group and the same virtual network, the First one with Windows 10 and 2nd with Ubuntu 22-24. (For this lab purpose, we can change authentication to password for easy access.)

---
![image](https://github.com/user-attachments/assets/478951f3-f7c5-4138-902a-326f464799d6)

The Next Step is to log into the Windows VM via remote desktop and install Wireshark to capture network protocols in action.

---
![image](https://github.com/user-attachments/assets/ed264da4-1adc-4007-b024-4340af18f126)

![image](https://github.com/user-attachments/assets/27b34fa4-66bd-4777-9c90-53e0e43afc88)

---
<h1>ICMP</h1>

Now that Wireshark is set up, let’s play around with some protocols, starting with ICMP, which doesn’t have a port number. We will type “icmp” in the filter at the top. Next, find the Linux machine’s private IP and try pinging it using ping (10.0.0.5) whatever the private IP address is since both machines are on the same network! Another observation is that we can also use ping 10.0.0.5 -t for a constant ping and use "Crtl + c' to kill it.  

![image](https://github.com/user-attachments/assets/42e1de88-f0f5-41e2-97ac-691fb53f5210)

---
We can also ping a website using  

![image](https://github.com/user-attachments/assets/42ed0b93-29fe-4667-908e-b142f722758a)

---
Next, we’re gonna set up a basic firewall! On your main device, go to the Linux virtual machine settings, find the network tab, open network settings, and create port rule ( add inbound security rule). In this port rule: change the setting to ICMPv4 (you’ll see the port range becomes “*” because ICMP doesn’t use ports), change the rule action to Deny, and set the priority to 290 so the VM knows to do this rule first!

![image](https://github.com/user-attachments/assets/ad4a89f2-3868-4c25-a7b9-9ba7dea1aa24)

![image](https://github.com/user-attachments/assets/c66a0589-a7fb-4594-a560-b034972166a6)

Check PowerShell again, and after a bit the ping will stop working because of the firewall, but if you delete the rule in your VM, the ping will work again!

![image](https://github.com/user-attachments/assets/160c19ab-1287-46da-ab2e-b46acc38c454)

<h1>SSH</h1>

Now we’re gonna use SSH, which is like a secret tunnel on port 22 to safely connect to another computer, so change your Wireshark filter to SSH, and when you use it in PowerShell it’ll ask for the password (don’t worry, it’s hidden) type whatever password you set for your linux VM, and once you’re in, we can do stuff like move files, control servers, and run commands!

![image](https://github.com/user-attachments/assets/2fcbb9f9-cfab-400d-a235-40f4c76b06a2)


We can run a few commands to crosscheck out information

![image](https://github.com/user-attachments/assets/1ebc8143-4f8d-4add-9ad6-19fe4e13d739)

---
<h1>DNS</h1>

Now we’re gonna check out DNS, which uses port 53 to turn website names into numbers for computers, so just change the Wireshark filter to DNS, use 'nslookup youtube.com' in PowerShell with any website (I used youtube.com), and you’ll see in Wireshark how the computer is asking for youtube’s IP address!

![image](https://github.com/user-attachments/assets/47f34f81-ec53-4679-91f5-c779bd71ba87)

---
<h1>RDP/TCP Port 3389</h1>

Next, we're going to check out how TCP port 3389, also called RDP (Remote Desktop Protocol), works, and you don't need PowerShell because we're already using RDP in the lab, so if you look at Wireshark, you'll see lots of data being sent back and forth between the client and the server.

![image](https://github.com/user-attachments/assets/91cbeefd-44d6-42af-89be-eff0e211ee3a)

---
<h1>HTTP</h1>

For our final protocol, we'll use HTTP, which runs on TCP port 80, and it's what web browsers use to talk to servers and load websites, search, update pages, and fetch resources like images, scripts, and stylesheets. You can see HTTP traffic in tools like Wireshark, where it shows how the browser requests and receives data from the server. HTTP is also used for background tasks like sending search queries and checking for new content, but when security is needed, HTTPS (which runs on port 443) is used instead of HTTP to keep things safe and private.

![image](https://github.com/user-attachments/assets/05c8972a-150d-44a3-b943-30add58cd8cc)



