<div id="header" align="center">
<img src="https://imgur.com/kpg2fwC.png" height="80%" width="80%" alt="header"/>
</div>
<h3>Description:</h3>
<body>The purpose of this project was to create an internal network via Virtualbox where traffic from a Windows 11 machine was monitored, and malicious traffic prevented. Through the use of Snort and it's community rules, log files were created when an alert was triggered and forwarded by a Splunk forwarder to an external SIEM server for further threat analysis.</body>


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
   <b>To facilitate communication between the internal and external server, VM3 had two network adapters enabled: 1 for an internal network named 'intnet', the other on NAT mode.  </b>
<img src="https://imgur.com/D8svMBk.png" height="100%" width="100%" alt=""/>                                                 
      </p>

      Challenges Faced: Can't ping snort machine and splunk server with each other

