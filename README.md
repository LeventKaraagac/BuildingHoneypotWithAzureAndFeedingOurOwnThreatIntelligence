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
<img src="https://i.imgur.com/dVcpadv.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/QU2pphM.png" alt="Project Steps"/>
<br>
2. Log Analytics Workspace: A Log Analytics workspace is created to collect and store the logs from the honeypot VM.
<img src="https://i.imgur.com/QTI9dBo.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/uNnActa.png" alt="Project Steps"/>
<br>
3. Microsoft Sentinel Deployment: Microsoft Sentinel is deployed on top of the Log Analytics workspace to function as the SIEM.
<img src="https://i.imgur.com/Ft5CRwT.png" alt="Project Steps"/>
<br>
<h3> Step 2: Data Connector and Detection Rule Configuration </h3>
1. Windows Security Events Connector: A Data Connector is configured to send Windows Security Events from the Windows 10 honeypot VM to the Sentinel instance. This ensures all relevant login and security event data is collected.
<img src="https://i.imgur.com/HHhnVCO.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/s2dns2W.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/wDmloHA.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/PJGSlWC.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/93cRnW6.png" alt="Project Steps"/>
<br>
2. Honeypot Alert Rule: A scheduled alert rule is created in Sentinel using KQL (Kusto Query Language) to trigger an incident whenever a successful RDP login occurs on the honeypot VM. This rule is a core component of the detection logic.
<img src="https://i.imgur.com/bWeLPoX.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/Cg0f9L0.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/zbJZ07i.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/FTBtXPf.png" alt="Project Steps"/>
<br>
3. Bastion Deployment and alert trigger checking: Deploy bastion within Azure and after logging in to the windows via rdp port 3389, check if the alert gets triggered.
<br>
<img src="https://i.imgur.com/sknD8p5.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/baumO2O.png" alt="Project Steps"/>
<br>
<h3> Step 3: MISP Threat Intelligence Platform Deployment</h3>
1. Ubuntu VM Creation: An Ubuntu Server 22.04 LTS VM is provisioned in Azure to host the MISP platform. Connect via SSH from Azure settings.
<img src="https://i.imgur.com/ZxbmkHj.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/e4UPHsn.png" alt="Project Steps"/>
<br>
2. Docker Installation: Docker is installed on the Ubuntu VM to simplify the deployment of MISP. Connect to the Ubuntu machine via Azure's CLI and write the following commands to download and configure docker. Lastly Verify that docker is configured.
<br>
<img src="https://i.imgur.com/oeTAVxP.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/gfhMQKW.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/Ya20RPY.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/ssPpupA.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/e2lsHab.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/K37bMFm.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/05hML7z.png" alt="Project Steps"/>
<br>
3. MISP Deployment: The MISP platform is deployed on the Ubuntu VM using Docker. For this, I will use the github documentation: github.com/MISP/misp-docker. After following the photos, don't forget to spin up this container by typing "sudo docker compose up" command.
<br>
<img src="https://i.imgur.com/09jGrGs.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/HOVHeQD.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/xJwiXCb.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/EKOB3Z6.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/5DXcPf7.png" alt="Project Steps"/>
<br>
4. MISP Configuration: MISP is configured after deployment, which includes setting up user accounts and adding official threat intelligence feeds. To get to the GUI of MISP, we must head to the IP address with the dedicated port running MISP. (Remember to make sure your ports are open and accessible so adjust firewall settings accordingly. After getting into MISP, change default credentials, import the json from MISP's official website to import the feeds to MISP. Follow these steps carefully as they are crucial.
<br>
<img src="https://i.imgur.com/2c0YgQV.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/COOmW3t.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/9fsvhpj.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/vuD3UK8.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/TJ9PWam.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/AYjYtiE.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/5fJvpkJ.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/5MsXEsm.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/hdOPkqW.png" alt="Project Steps"/>
<br>
<h3> Step 4: Sentinel & MISP Integration</h3>
1. Azure API Key for MISP and Function App Creation: An API key is generated in MISP to allow external applications, such as a Function App, to access its data. First we must download the data connected specifically for MISP though. Then a Python-based Function App is created in Azure to serve as the bridge between MISP and Sentinel. The Function App is configured to use the MISP API to pull threat intelligence data and feed it directly into Microsoft Sentinel. This process enriches the SIEM with custom threat data.
<br>
<img src="https://i.imgur.com/drFETh8.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/Dtg1CW9.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/0cjhplE.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/5mueECv.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/d0dfMdb.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/hmRDZgd.png" alt="Project Steps"/>
<br>
2. Sentinel Threat Intelligence Creation: Within Sentinel, a threat intelligence feed is created that receives data from the Function App, making the MISP data available for detections and analytics.
<br>
<img src="https://i.imgur.com/T2md5ga.png" alt="Project Steps"/>
<br>
<img src="https://i.imgur.com/IfD3iZb.png" alt="Project Steps"/>
<br>
3. Couple hours after what Sentinel looked like:
<br>
<img src="https://i.imgur.com/Q8XyjOK.png" alt="Project Steps"/>
<br>
</p>



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
