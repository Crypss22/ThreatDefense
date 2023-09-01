<div id="header" align="center">
<img src="https://imgur.com/kpg2fwC.png" height="80%" width="80%" alt="header"/>
</div>
<h3>Description:</h3>
<body>The purpose of this project was to create an internal network via Virtualbox and simulate suspicious network activity from within that internal network onto a Windows 11 machine. The network the Windows 11 machine was operating on was monitored utilizing Snort and any malicious activity was logged and prevented through Snort's inline mode. After creating logs, a Splunk forwarder was used to relay them to an external SIEM server for further threat analysis.</body>
   </br>
   </br>
<b>Throughout the course of this project, some roadblocks I ran into were:</b></br>
   - Creating another virtual adapter for the internal network in order to allow the flow of communication between the VMs.</br>
   - Creating a NAT network to place both VMs 3 & 4 on in order to allow communication between the internal and external network.
</p>


<h2>Utilities Used</h2>
<b>
- Splunk</br>
- Snort
</b>
<h2>Environments Used </h2>
<b>
- VM1 Kali Linux</br>
- VM2 Windows 11</br>
- VM3 Ubuntu w/ Snort and Splunk Forwarder</br>
- VM4 Ubuntu Splunk Server</br>
</b>
<img src="https://imgur.com/pqYdQTW.png" height="80%" width="80%" alt="Network Diagram"/>
<img src="https://imgur.com/F6XUEbD.png" height="45%" width="45%" alt="vm addresses"/>

<h2>Project walk-through:</h2>
   <p align="center">
      To facilitate communication between VMs on the internal network, Adapter #2 was created, enabling the DHCP server to distribute those IPs amongst the VMs. From there, each virtual machine was manually assigned an IP address within that subnet. VM3 was configured with 2 network profiles allowing it to communicate with both the internal network (2nd screenshot), and VM4 on the outside through NAT.
   <img src="https://imgur.com/6OBoGI3.png" height="45%" width="45%" alt="Adapter #2"/> 
   <img src="https://imgur.com/k4Q3nGw.png" height="55%" width="55%" alt="VM3 2 network profiles"/>
</p>
</br>
   <p align="center">
      Snort was installed onto VM3 and the configuration file, snort.conf, was edited utilizing vim text editor. The HOME_NET variable was given the subnet of the internal network. 
   </br>
    <img src="https://imgur.com/gCfjxgN.png" height="75%" width="75%" alt="snort.conf"/>  
      </p>
