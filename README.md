<div id="header" align="center">
<img src="https://imgur.com/kpg2fwC.png" height="80%" width="80%" alt="header"/>
</div>
<h3>Description:</h3>
<body>The purpose of this project was to create an internal network via Virtualbox where traffic from a Windows 11 machine was monitored, and malicious traffic prevented. Through the use of Snort and it's community rules, log files were created when an alert was triggered and forwarded by a Splunk forwarder to an external SIEM server for further threat analysis.</body>
   </br>
   </br>
<p>Throughout the course of this project, I ran into several roadblocks while configuring the internal network. My first issue was enabling all virtual machines on the internal network to communicate with one another. I was under the assumption that as soon as they were placed on the same internal network in the settings of each machine, manually assigned an ip address within the subnet, that they would be able to communicate. What I had figured out after not being able to ping either machine from one another was that a host-only network adapter had to created and the DHCP server configured.
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

<h2>Project walk-through:</h2>
   <p align="center">
      To facilitate communication between VMs on the internal network, Adapter #2 was created and the DHCP server enabled. From there, each virtual machine was manually assigned an IP address within that subnet (LEFT). VM4 was configured with 2 network profiles, allowing it to communicate with both the internal network, and the internet through NAT (RIGHT).
   <img src="https://imgur.com/6OBoGI3.png" height="45%" width="45%" alt="Adapter #2"/> 
   <img src="https://imgur.com/EbsMoRD.png" height="45%" width="45%" alt="VM3 2 network profiles"/>
   <img src="https://imgur.com/hUVbCAq.png" height="60%" width="60%" alt="vm addresses"/>
</p>
</br>
</br>
</br>

<p align="center">
   To facilitate communication between the internal and external server, VM3 had two network adapters enabled: 1 for an internal network named 'intnet', the other on NAT mode.
<img src="https://imgur.com/D8svMBk.png" height="100%" width="100%" alt=""/>                                                 
      </p>

