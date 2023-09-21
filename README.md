<div id="header" align="center">
<img src="https://imgur.com/kpg2fwC.png" height="80%" width="80%" alt="header"/>
</div>
<h3>Description:</h3>
<body>The purpose of this project was to create an internal network via Virtualbox and detect and log malicious activity from within the internal network. Network traffic was monitored utilizing Snort and any malicious activity was logged and prevented through Snort's inline mode. After creating logs, a Splunk forwarder was used to relay them to an external SIEM server for further analysis.</body>
   </br>
   </br>
<b>During the creation of this project, a roadblock I ran into was:</b></br>
Figuring out that although the virtual machines were placed on the same internal network through Virtualbox's network settings, that they were still not able to communicate with each other. I had manually assigned them IPs within the same subnet, but wasn't aware that I needed to create a network adapter in order to act as a DHCP server. Once that was figured out, I switched all machines on the internal network to automatically assign, receiving IPs from that DHCP server.
<h2>Software Used</h2>
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
<b>
   <p align="center">
      To facilitate communication between VMs on the internal network, Adapter #2 was created, enabling the DHCP server to distribute those IPs amongst the VMs. From there, each virtual machine was manually assigned an IP address within that subnet. VM3 was configured with 2 network profiles allowing it to communicate with both the internal network, and VM4 on the outside through NAT (2nd screenshot).
   <img src="https://imgur.com/6OBoGI3.png" height="45%" width="45%" alt="Adapter #2"/> 
   <img src="https://imgur.com/k4Q3nGw.png" height="55%" width="55%" alt="VM3 2 network profiles"/>
</p>
</br>
   <p align="center">
      Snort was installed onto VM3 and the configuration file, snort.conf, was edited utilizing vim text editor. The HOME_NET variable was given the subnet of the internal network. 
   </br>
    <img src="https://imgur.com/gCfjxgN.png" height="75%" width="75%" alt="snort.conf"/>  
      </p>
      </br>
      <p align="center">
         The IP address in which the Splunk Forwarder would be forwarding it's logs to was added utilizing port 9997 which is used for splunk-to-splunk communication. Port 9997 is Splunk's default port for the transfer of data and ensures secure, reliable, and       encrypted transfer of data.
   </br>
    <img src="https://imgur.com/Lhl2YOf.png" height="75%" width="75%" alt="snort.conf"/>  
      </p>
      <p align="center">
         Next, I added the log file that Splunk would be forwarding to the server and that was the Snort alert file as seen below. Directly after that, I went back one directory and jumped into /etc/apps/search/local as root and added lines 1, 2, and 5-7 to assist Splunk in it's indexing process.
   </br>
    <img src="https://imgur.com/YkW11FB.png" height="75%" width="75%" alt="snort.conf"/>  
      </p>
</b>
