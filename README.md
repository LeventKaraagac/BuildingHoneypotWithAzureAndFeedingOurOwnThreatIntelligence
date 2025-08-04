<p align="center">
<img src="https://i.imgur.com/xMrbW8Q.png" alt="Basic Home SOC Lab Steps"/>
</p>

<br>
<h1>Building a Honeypot With Azure And Feeding Our Own Threat Intelligence</h1>

<h2>Project Description</h2>
This project details the creation of a honeypot environment using Microsoft Azure. The goal is to capture attack data and feed it into a custom threat intelligence platform. The architecture involves deploying a Virtual Machine (VM) as the honeypot, using Microsoft Sentinel as the SIEM to collect security events, and integrating MISP (Malware Information Sharing Platform) for threat intelligence. The project demonstrates the full workflow from setting up the honeypot to gathering threat data, creating a custom threat intelligence feed, and using it for enhanced detection in Sentinel.


<h2>Environments and Technologies Used</h2>

- <b>Cloud Platform:</b> Microsoft Azure
- <b>SIEM:</b> Microsoft Sentinel
- <b>Honeypot:</b> Windows 10 VM
- <b>Threat Intelligence Platform:</b> MISP (open source)
- <b>Virtualization:</b> Docker
- <b>Data Connector:</b> Azure Data Connector for Windows Security Events
- <b>Additional Tools:</b> Azure Bastion, Azure CLI, Function App


<h2>Operating Systems Used</h2>

- <b>Windows 10:</b> Used as the honeypot VM.
- <b>Ubuntu Server 22.04 LTS:</b> Used for the VM hosting the MISP threat intelligence platform.



<h2>Overview of Steps</h2>
1. <b>Honeypot VM Setup:</b> Creation of a Windows 10 Virtual Machine in Microsoft Azure with RDP port 3389 left open to the internet to act as a honeypot.
<br>
2. <b>Sentinel Deployment:</b> Creation of a Log Analytics workspace and deployment of Microsoft Sentinel to serve as the SIEM.
<br>
3. <b>Data Connector Configuration:</b> Setting up a Data Connector to send security events from the Windows VM to the Sentinel instance for log collection.
<br>
4. <b>Honeypot Alert Rule Creation:</b> Creation of a scheduled alert rule in Sentinel to trigger an incident whenever a successful RDP login occurs on the honeypot VM.
<br>
5. <b>MISP Threat Intelligence Setup:</b> Deploying MISP on an Ubuntu VM using Docker, configuring it, and setting up official threat intelligence feeds.
<br>
6. <b>MISP & Sentinel Integration:</b> Creating a Function App and API key to connect MISP to Sentinel, allowing the threat intelligence data to be fed into the SIEM.
<br>
7. <b>Verification:</b> Testing the entire workflow by RDP'ing into the honeypot to trigger an incident in Sentinel and verifying that the MISP threat intelligence is being used effectively.
<br>

<p>
<h2>Project Walkthrough</h2>
<h3> Step 1: Honeypot VM Setup in Microsoft Azure </h3>
1. Honeypot VM Creation: A Windows 10 Virtual Machine is created in Microsoft Azure. The RDP port 3389 is left open to the internet to serve as the honeypot.
<br>
<img src="" alt="Project Steps"/>
<br>

<h3> Step 2: Network Configuration</h3>


<h2>Key Learning/Reflections</h2>
- <b>Cloud Infrastructure Management:</b> Gained experience in deploying and managing virtual machines, firewalls, and other resources within Microsoft Azure.
<br>
- <b>SIEM and EDR Integration:</b> Learned how to connect a VM to a SIEM (Sentinel) and configure data connectors to ingest security events.
<br>
- <b>Threat Hunting & Rule Creation:</b> Developed skills in creating custom analytic rules in Sentinel using KQL (Kusto Query Language) to detect specific malicious activities, such as successful RDP logins.
<br>
- <b>Open-Source Integration:</b> Successfully deployed and configured an open-source threat intelligence platform (MISP) using Docker, demonstrating the ability to integrate disparate tools.
<br>
- <b>API-Driven Automation:</b> Gained hands-on experience in using APIs to connect platforms, specifically by creating a Function App and client secret to pull threat intelligence from MISP into Sentinel.
<br>
- <b>Hands-on Security Experience:</b> Acquired practical knowledge of building a controlled honeypot environment to safely capture and analyze real-world attack data.

<h2>Conclusion</h2>
This project successfully established a comprehensive honeypot environment in Microsoft Azure, integrated with a powerful SIEM and a custom threat intelligence feed. It demonstrated a full-cycle approach to threat detection, from intentionally exposing a vulnerable system to collecting attack data, creating custom detection rules, and enriching that data with open-source threat intelligence. The skills acquired in cloud deployment, system integration, and automation are highly valuable for a career in cybersecurity, providing a robust foundation for building advanced security solutions.
