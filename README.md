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
Within Wireshark, filter for ICMP (Internet Control Message Protocol) traffic. 
</p>

![NWSG 7](https://github.com/Jacob-Oq/azure-network-protocols/assets/150084528/df4b6207-5156-49e2-a59b-c9458c9d1f07)

<p>
Open PowerShell to execute a command called ping. Ping utilizes ICMP, which is used by devices in a network to communicate problems within data transmition. We can use ping to see if it is possible communicate with the Ubuntu VM using its private IP address and with google.com.
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
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
