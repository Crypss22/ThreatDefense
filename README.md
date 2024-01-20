<div id="header" align="center">
<img src="https://imgur.com/kpg2fwC.png" height="80%" width="80%" alt="header"/>
</div>
<h3>Description:</h3>
For this project I wanted to put to use my knowledge of both Splunk and Snort. I wanted to dive deeper into using both in a practical setting and one idea that came to mind was combining both tools to monitor malicious network traffic from within the internal network.
</br>
</br>
I setup this homelab using Virtualbox and performed reconnaissance from within the internal network to simulate an attacker who has already accessed the network and is looking to pivot to another machine, continuing their attack. I used Snort to actively monitor the network, and forward it utilizing a Splunk Forwarder to an external server for real-time analysis.
</br>
</br>
This project helped me to better understand how multiple security solutions can be integrated with one another and increase the security of a network.
   </br>
   </br>
<h2>Software Used</h2>
<b>
- Splunk</br>
- Snort</br>
- Nessus
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
</br>
</br>
      <img src="https://imgur.com/6OBoGI3.png" height="45%" width="45%" alt="Adapter #2"/> 
</p>
</br>
   <h3 align="center">Configuration of Snort and Splunk Forwarder</h3>
</br>
   <p align="center">
      Snort was installed onto VM2 and the configuration file, snort.conf, was edited utilizing vim text editor. The HOME_NET variable was given the subnet of the internal network. 
   </br>
   </br>
    <img src="https://imgur.com/gCfjxgN.png" height="75%" width="75%" alt="snort.conf"/>  
      </p>
      </br>
   <p align="center">
         The IP address in which the Splunk Forwarder would be forwarding it's logs to was added utilizing port 9997 which is used for splunk-to-splunk communication. Port 9997 is Splunk's default port for the transfer of data and ensures secure, reliable, and       encrypted transfer of data.
   </br>
   </br>
    <img src="https://imgur.com/Lhl2YOf.png" height="75%" width="75%" alt="splunk-forwarder"/>  
      </p>
</br>
   <p align="center">
         Next, I added the log file that Splunk would be forwarding to the server and that was the Snort alert file as seen below. Directly after that, I went back one directory and jumped into /etc/apps/search/local as root and added lines 1, 2, and 5-7 to assist Splunk in it's indexing process.
   </br>
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
   </br>
    <img src="https://imgur.com/vhFfjAx.png" height="75%" width="75%" alt="splunk acc config"/>  
      </p>
</br>
<p align="center">
      I then configured splunk to listen on port 9997 and confirmed it as listening on that port by running the following commands. For the sole purpose of this project, please pay no mind to the weak login credentials. 
   </br>
   </br>
    <img src="https://imgur.com/G8sUy1n.png" height="45%" width="45%" alt="splunk listen port"/> 
    <img src="https://imgur.com/lTRasF2.png" height="45%" width="45%" alt="splunk listen port confirm"/>
      </p>
</br>
<p align="center">
      Finally, our splunk server was accessed through port 8000. From there I was able to access the Search and Reporting app and confirm the logs were being forwarded through the Data Summary button.
   </br>
   </br>
    <img src="https://imgur.com/lcJnNvJ.gif" height="90%" width="90%" alt="data summary"/>
      </p>
</b>
</br>
</br>

<h3 align="center">Sending & Detecting Attacks</h3>
</br>
<b>
<p align="center">
      To confirm Snort was monitoring network activity, I sent some pings from the attackbox to the target. Reconnaissance is crucial to mapping out an internal network's topology and an attacker may do so to scout a potential endpoint in which they can pivot into. Shown below is the Kali attackbox sending pings and those pings being monitored realtime through Splunk.
   </br>
   </br>
    <img src="https://imgur.com/E8RxWlE.png" height="50%" width="50%" alt="attackbox sending pings"/>
</br>
   Attackbox
</br>
   <img src="https://imgur.com/mxx0XGS.png" height="90%" width="90%" alt="splunk monitoring pings"/>
</br>
   Splunk server
      </p>
</br>
   
<p align="center">
     After confirming Snort was actively monitoring the network, I conducted vulnerability scans on the target machine. For this portion of the project, I utilized Nessus, a popular vulnerability scanner with a large database of known vulnerabilities.
   </br>
   </br>
    <img src="https://imgur.com/SQFsQqi.png" height="90%" width="90%" alt="nessus install"/>
      </p>
<p align="center">
     Once on Nessus, I conducted an advanced scan on the target which provides over 25k+ tests in 30+ plugins.
   </br>
   </br>
    <img src="https://imgur.com/a7pII2Q.gif" height="90%" width="90%" alt="nessus advanced scan"/>
      </p>
<p align="center">
   </br>
    <img src="https://imgur.com/nepTrol.png" height="90%" width="90%" alt="nessus advanced scan complete"/>
    </br>
    The scan was completed and it returned it's results with no detected vulnerabilities. Although the scan returned no vulnerabilities, it's important to note that Nessus is not the say all, be all. Since new exploits are constantly being created and discovered, Nessus' database must be updated regularly to detect them.
      </p>
      </br>
      </br>
<p align="center">
     As the advanced scan was being conducted, Splunk was receiving logs from the forwarder in real-time. For an in-depth event summary, I used a Splunk app called Snort Alert for Splunk.
   </br>
   <img src="https://imgur.com/dNBPNUx.png" height="30%" width="30%" alt="snort alert for splunk logo"/>
   </br>
   </br>
   <img src="https://imgur.com/pAPfXbM.gif" height="90%" width="90%" alt="snort alert for splunk"/>
   </br>
   </br>
   The Snort Alert for Splunk app provided an organized, clean looking interface, and was quickly easy to understand. As seen above, it organized the top 10 classifications of attacks received from the Snort IDS; Misc activity being number 1, at a 269 event count. If we go ahead and click on that, it brings us to the Search and Reporting app with a focus on just those events. Those Misc activity events were from ICMP traffic.
   </br>
   </br>
   <img src="https://imgur.com/i0FNG2R.png" height="90%" width="90%" alt="misc activity"/>
      </p>
   </br>
   </br>
</b>

<h3>In conclusion:</h3>
With the development and implementation of efficient alerting and detection strategies, a strong proactive approach to monitoring systems is taken. Although threat actors continue to exploit systems through a plethora of ways, damage, if any, can be curbed.
The goal of this project was to not only create a hands-on experience, but to provide the reader with a perspective into the ease of successfully and seamlessly integrating Snort and Splunk, ultimately bolstering a network's security and providing an analyst with real-time monitoring and forensic capabilities.
</br>
</br>
<h3>Resources:</h3>
<p>
https://community.splunk.com/t5/Getting-Data-In/How-to-activate-forwarder-server/m-p/368584/thread-id/66933
</p>
