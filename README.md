# AD-Project

## Objective

The goal of this project was to create a basic Active Directory (AD) environment, simulate attacks from Kali Linux, and configure Splunk to collect and analyze telemetry from target machines.

## Lab Environment
- **Windows 10 Client:** Splunk Universal Forwarder + Sysmon
- **Windows Server:** Active Directory Domain Services (ADDS) + Splunk Forwarder + Sysmon
- **Ubuntu Server:** Splunk Enterprise (SIEM)
- **Kali Linux:** Attack platform

## Skills Learned

- Setting up Active Directory Domain Services (ADDS)
- Installing and configuring Splunk on Ubuntu Server
- Forwarding logs from endpoints to a SIEM
- Configuring Sysmon for enhanced telemetry
- Analyzing and interpreting network logs
- Recognizing common attacker techniques
- Conducting brute force attacks for testing SIEM detection

## Tools Used
- **VirtualBox** – VM creation and NAT network setup
- **Active Directory Domain Services (ADDS)** – Domain and user account creation
- **Splunk Enterprise** – Log ingestion and analysis
- **Sysmon** – Windows system monitoring
- **Crowbar** – Brute force attack tool
- **Atomic Red Team (ART)** – MITRE ATT&CK simulation framework

## Workflow Overview
1. Install Windows Server 2022 and configure it as a Domain Controller.
2. Join a Windows 10 client to the Active Directory domain.
3. Create users, groups, and organizational units within Active Directory.
4. Install Splunk Universal Forwarders on both VMs.
5. Forward logs (Security, System, Application) to Splunk.
6. Build dashboards in Splunk to visualize AD activity.
7. Simulate basic attack scenarios (e.g., brute force, privilege escalation).
8. Capture and analyze events in Splunk.
9. Configure alerts in Splunk based on suspicious activity.
10. Document manual review and response actions.

## Steps

![adproject-network-diagram](https://github.com/user-attachments/assets/d47fdf38-669e-4452-ab0c-c6fc44962f0e)

**Figure 1 – Lab Network Topology:** Four VirtualBox VMs — Splunk Server, Active Directory, Windows 10 Client, and Kali Linux — connected via NAT for attack simulation and log analysis.

![00-installer-config yaml](https://github.com/user-attachments/assets/9114d4eb-ec00-475f-a53b-b45f239f2cd1)

**Figure 2 - Splunk Server Network Configuration:** Static IP set on Splunk server as per network diagram. Default gatway configured for NAT network. Google DNS used as no DNS server setup for this lab.

![ip -a Splunk](https://github.com/user-attachments/assets/b885d029-8f0e-4871-8ad3-d0dc5f6ff317)

**Figure 3 – Splunk Server IP Verification:** Output from ip -a confirming the Splunk server is using the static IP address 192.168.10.10/24 as configured.

![splunk-login-page](https://github.com/user-attachments/assets/9e32575c-ccff-4008-aa21-ace79b00d572)

**Figure 4 – Splunk Web Interface Access:** Successful connection to the Splunk Enterprise GUI from the Windows 10 client machine, confirming network and service availability.

![ADDC Settings](https://github.com/user-attachments/assets/62151b93-3197-4502-9e30-9c8b71e49c81)

**Figure 5 – Active Directory Server Configuration:** Properties of ADDC01 showing it is joined to the ADProject.local domain with the correct static IP address 192.168.10.7.

![IT User](https://github.com/user-attachments/assets/eba3b8cd-b971-4558-a000-65e9ec6f6dc7)

**Figure 6 - AD Group 1:** IT OU created and user added into AD.

![HR User](https://github.com/user-attachments/assets/87dbcc38-cbb9-40de-a7ba-24fdc04ee66e)

**Figure 7 - AD Group 2:** HR OU created and user added into AD.

![inputs conf](https://github.com/user-attachments/assets/86a9d416-9373-4cd6-bd50-fdde22dcbc7c)

**Figure 8 - input.conf:** New variant of inputs.conf created for Splunk index (Client Machine). The Splunk Universal Forwader will push the events listed in this file over to the Splunk server. This was also setup on the DC as you will see with Figure 13 where two hosts appear in the Splunk logs.

![inputs conf location](https://github.com/user-attachments/assets/05440b99-c07d-41f2-861c-64f1bc632237)

**Figure 9 - input.conf location change:** Defualt location for inputs.conf is C:\Program Files\SplunkUniversalForwarder\etc\system\default which needs to stay as is. A new inputs.conf file was created in C:\Program Files\SplunkUniversalForwarder\etc\local which Splunk will look to. Note that anytime the inputs.conf file is changed the Universal Forward service needs to be restarted.

<img width="575" height="314" alt="image" src="https://github.com/user-attachments/assets/d44f7807-b992-4ac4-bb5d-f62e2c5d8ba0" />

**Figure 10 - Splunk Forwarder:** Within the SplunkForwarder service the Log On tab needs to be changed to use Local System Account otherwise it will not have all the required permissions.

![endpoint-index](https://github.com/user-attachments/assets/407d2de4-fce4-401d-968d-b621dee412b8)

**Figure 11 - endpoint index created:** In Figure 8 the inputs.conf file has the index listed as endpoint. This has to be created within Splunk otherwise the logs will not show.

![receiving-9997](https://github.com/user-attachments/assets/51bbd9ba-8525-47f8-97cf-df6842d00275)

**Figure 12 - Setting up receiving port in Splunk:** By default the port for receiving logs is 9997 and this is what is used in this lab. 

![endpoints-pc-ad](https://github.com/user-attachments/assets/c37888c2-1a91-4ed0-8525-ed6647dc91d8)

**Figure 13 - Confirming hosts visile in Splunk:** Both the DC and the client are forwarding logs into Splunk.

![rdp-win10-client](https://github.com/user-attachments/assets/b075f969-92e6-4db3-a1f0-a6528bda2280)

**Figure 14 - Enabling RDP on client machine:** By enabling RDP this will help with the next steps where the brute force attack comes into play.

![rockyou-passwords-list](https://github.com/user-attachments/assets/e3ff7c98-3b11-4b1f-9125-7f60ec18c081)

**Figure 15 - Crowbar:** Beginning to use Crowbar and generating passwords file for brute force attack

![adding-password](https://github.com/user-attachments/assets/110429e8-2b22-45c3-8716-1bb141de78be)

**Figure 16 - Password file**: This is the example password file that will be used for the 

![SplunkEventJNeutron](https://github.com/user-attachments/assets/f9597e96-491f-4ded-8cba-c86f5dc38cf9)

**Figure 17 - JNeutron logs:** Searching specifically for JNeutron user logs

![EventCode4625](https://github.com/user-attachments/assets/a8e3661b-7b7a-4024-8a6a-745bdeadf047)

**Figure 18 - Failed login attemps:** Event ID referencing failed login attempts

![FailedLoginAttempts](https://github.com/user-attachments/assets/4e902508-2b82-4f3a-b6a9-c760f76d544e)

**Figure 19 - Splunk logs for failed login attempts:** Telemetry for failed login attempts

![FullEventLogBruteForce](https://github.com/user-attachments/assets/6799dea0-1fa4-4e0a-a882-f4ece2bac066)

**Figure 20 - Brute Force Splunk logs:** Kali machine used to brute force the password with Crowbar. Spunk logs verify the attempts showing 'Unknown username or bad password' and logs show the IP of the Kali machine which is where these attempts are originating from.

![InstallingART](https://github.com/user-attachments/assets/f099f10c-9ebd-4ea7-9524-6f6f3c20f92f)

**Figure 21 - Installing Atomic Red Team:** Installed Atomic Red Team via PowerShell using the official script from Red Canary. Included NuGet provider setup and confirms successful installation of Invoke-AtomicTest for executing atomic tests.

![AtomicTestT1136 001-LocalUser](https://github.com/user-attachments/assets/9505a5c6-e3b3-4255-b4b4-1ffedd728ff1)

**Figure 22 - : T1136.001:** Demonstrates multiple methods of local account creation using Command Prompt, PowerShell, and .NET, aligned with MITRE ATT&CK T1136.001. Includes both standard and administrator account creation, highlighting detection challenges across techniques.

![DetectingT1136 001-NewLocalUser](https://github.com/user-attachments/assets/49fd45ab-7914-4ecc-b1e5-9c2e1fab6d6f)

**Figure 23 - Local account detection:** The Splunk logs now show creation of the new account. This would help in real life scenarios by alerting to a potential breach in a network.

## Outcomes
- Successfully built a working AD environment with Splunk monitoring
- Simulated real-world brute force and persistence attacks
- Verified detection of attacker activity via SIEM
- Gained hands-on experience with both defensive and offensive security tools

