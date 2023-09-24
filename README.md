<div id="header" align="center">
<img src="https://imgur.com/kpg2fwC.png" height="80%" width="80%" alt="header"/>
</div>
<h3>Description:</h3>
For this project I wanted to use my knowledge of Splunk, and my knowledge of Snort from TryHackMe. I wanted to dive deeper into using both in a practical setting and one idea that came to mind was combining both tools to monitor malicious network traffic from within the internal network.
</br>
</br>
I setup this homelab using Virtualbox and conducted some simple reconnaissance attacks that might raise concerns originating from inside the internal network. I then used Snort to monitor the network traffic and forward it utilizing a Splunk Forwarder to an external Splunk server.
</br>
</br>
This project helped me to better understand how Snort could be integrated with Splunk and how both tools can assist in the security of a network.
   </br>
   </br>
<h2>Software Used</h2>
<b>
- Splunk</br>
- Snort
</b>
<h2>Environments Used </h2>
<b>
- VM1 Kali Linux</br>
- VM2 Ubuntu w/ Snort & Splunk Forwarder</br>
- VM3 Splunk Server</br>
</b>
<img src="https://imgur.com/abHHJic.png" height="80%" width="80%" alt="Network Diagram"/>

<h2>Project walk-through:</h2>
<b>
   <p align="center">
      To facilitate communication between VMs on the internal network, Adapter #2 was created, enabling the DHCP server to distribute those IPs amongst the VMs. From there, each virtual machine was manually assigned an IP address within that subnet. VM2 was configured with 2 network profiles allowing it to communicate with both the internal network, and the external Splunk server.
   <img src="https://imgur.com/6OBoGI3.png" height="45%" width="45%" alt="Adapter #2"/> 
</p>
</br>
   <h3 align="center">Configuration of Snort and Splunk Forwarder</h3>
</br>
   <p align="center">
      Snort was installed onto VM2 and the configuration file, snort.conf, was edited utilizing vim text editor. The HOME_NET variable was given the subnet of the internal network. 
   </br>
    <img src="https://imgur.com/gCfjxgN.png" height="75%" width="75%" alt="snort.conf"/>  
      </p>
      </br>
      <p align="center">
         The IP address in which the Splunk Forwarder would be forwarding it's logs to was added utilizing port 9997 which is used for splunk-to-splunk communication. Port 9997 is Splunk's default port for the transfer of data and ensures secure, reliable, and       encrypted transfer of data.
   </br>
    <img src="https://imgur.com/Lhl2YOf.png" height="75%" width="75%" alt="splunk-forwarder"/>  
      </p>
      <p align="center">
         Next, I added the log file that Splunk would be forwarding to the server and that was the Snort alert file as seen below. Directly after that, I went back one directory and jumped into /etc/apps/search/local as root and added lines 1, 2, and 5-7 to assist Splunk in it's indexing process.
   </br>
    <img src="https://imgur.com/YkW11FB.png" height="75%" width="75%" alt="monitoring file"/>  
      </p>
</br>
</br>
<h3 align="center">Splunk Server Configuration</h3>
</br>
<p align="center">
      On the server, Splunk Enterprise was downloaded and moved to the /opt directory. From there I accessed splunk's /bin directory, started it up and made an account.
   </br>
    <img src="https://imgur.com/vhFfjAx.png" height="75%" width="75%" alt="splunk acc config"/>  
      </p>
<p align="center">
      I then configured splunk to listen on port 9997 and confirmed it as listening on that port by running the following commands. For the sole purpose of this project, pay no mind to the weak login credentials. 
   </br>
    <img src="https://imgur.com/G8sUy1n.png" height="45%" width="45%" alt="splunk listen port"/> 
    <img src="https://imgur.com/lTRasF2.png" height="45%" width="45%" alt="splunk listen port confirm"/>
      </p>
A resource I utilized that assisted me in setting up the communication between the splunk forwarder and server was this thread from the Splunk community.
https://community.splunk.com/t5/Getting-Data-In/How-to-activate-forwarder-server/m-p/368584/thread-id/66933
</br>
</br>
   
<b>Although the setup was pretty basic, a roadblock I ran into was:</b></br>
Figuring out that although the virtual machines were placed on the same internal network through Virtualbox's network settings, that they were still not able to communicate with each other. I had manually assigned them IPs within the same subnet, but wasn't aware that I needed to create a network adapter in order to act as a DHCP server. Once that was figured out, I switched all machines on the internal network to automatically assign, receiving IPs from that DHCP server.
