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

<h2>Contents</h2>

<p>Within Azure, I created two VMs within the same virtual network to ensure that they are able to communicate with each other. One VM will have Windows 10 Pro while the other uses Ubuntu. The Windows VM will connect to the other via the command line/PowerShell.</p>

<h2>Actions and Observations</h2>
<p>
Using Remote Desktop Connection, we connect to the Windows VM using its public IP address. From there, install Wireshark in order to begin inspecting traffic.
</p>

![NWSG 4](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/953dfd89-07f8-44d6-974d-5e6db7149052)

<br />
<p>
Within Wireshark, filter for "ICMP" (Internet Control Message Protocol) traffic. 
</p>

![NWSG 7](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/df4b6207-5156-49e2-a59b-c9458c9d1f07)

<p>
Open PowerShell to execute a command called "ping". Ping utilizes ICMP, which is used by devices in a network to communicate problems within data transmition. We can use ping to see if it is possible communicate with the Ubuntu VM using its private IP address and with google.com.
</p>

![NWSG 8](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/39aa1e2f-0d2d-4069-9521-51485d0c4774)

![NWSG 9](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/b1b10935-5f98-49ab-b747-094922eed292)

![NWSG 10](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/67727957-08c6-4280-801b-0dd204eac179)


<p>
Using a perpetual ping to the Ubuntu VM we can see how network security groups work. To execute the perpetual ping enter the command: ping -t (ip address). 
</p>

![NWSG 11](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/fc41483c-a075-41e7-9784-1e38d1d853ed)


<br />
<p>
Now back at the Azure portal, open the networking settings for the Ubuntu VM and add an inbound security rule to block ICMP traffic. Make sure to have the priority higher than SSH (300) to ensure the rule applies first. 
</p>

![NWSG 13](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/3a08b883-b333-4d3f-bd24-3526dcc89cd4)

![NWSG 14](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/f37d331d-8347-4184-98ca-dd87ec8cfdc5)

![NWSG 15](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/4227be6b-18bf-454e-9ab2-24549d2a81e6)

<br />
<p>
Head over to the Windows VM. Notice the ICMP traffic is blocked now that the inbound security rule is in place.
</p>

![NWSG 16](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/f378f200-096a-4684-974f-ed6273ea124c)

<p>
After changing the rule to allow traffic again, the perpetual ping resolves without timing out. 
</p>

![NWSG 17](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/bcfab96d-1eaa-4b4b-a904-8c4ed7bbc501)

<br />
<p>Now let's examine SSH traffic. Log into the Ubuntu server via PowerShell with the "ssh" command.</p> 
  
![NWSG 20](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/298f6970-da16-41a2-a838-d0847f79f830)

![NWSG 21](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/90d034d6-41b4-4d8c-addc-cbb42bbea6d5)

![NWSG 22](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/cf268b88-b713-43d8-bfb2-f6521a5276a4)

<p>
In Wireshark, we can filter the traffic with "tcp.port == 22". While logged into the Ubuntu server, the session is logged in Wireshark with each command used. </p>

![NWSG 25](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/053db461-2634-4840-9222-bb8b858c878a)

<br />
<p>After examining SSH traffic, exit the Ubuntu server in order to filter for DHCP traffic.</p>

![NWSG 26](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/605ce18c-b147-43a0-9d53-5009c291751b)

We can attempt to issue a new IP address from the VM to see what happens. The command "ipconfig /renew" will attempt to issue a new IP address and will temporarily disrupt the connection for a few seconds. After reconnecting, the resulting traffic is shown in Wireshark. 

![NWSG 27](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/d186277c-cafc-449a-9efa-2251f4f3d3e6)

<br />
<p>To observe DNS traffic, we can use "dns" or "udp.port == 53" in the search area to filter for it and the command nslookup.</p>

![NWSG 28](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/508f9a14-2990-448d-812e-f25485f7773c)

![NWSG 29](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/ee9ec890-182e-40d5-b95e-9ab0d93b01ef)

![NWSG 30](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/55d9c2d5-d341-4a65-8f53-d721317a298a)

![NWSG 31](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/65d12cc5-6028-4a89-b6c1-a3ecdb79a5fb)


<br />
<p>We can also observe RDP traffic. The filter for Wireshark is "tcp.port == 3389". There will be non-stop traffic because RDP is constantly showing a live stream from one computer to another and thus traffic is always transmitted. </p>

![NWSG 32](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/ef83965c-a7f8-45e0-9db8-23936450da97)

<h2>Final Thoughts</h2>

The purpose of this lab is to see how different protocols and ports are utilized in a network between devices. While this lab does not exactly allow troubleshooting, we still gather pertinent information. While utilizing different tools like Wireshark and the command line we see how traffic flows in a network through ports and protocols.
