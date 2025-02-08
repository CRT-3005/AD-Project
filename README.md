# AD-Project

## Objective

This Project aimed to create a basic AD environment, utilise the user accounts to perform attacks on from Kali and have Splunk configured to generate telemetry from the target machines. 
In total there were 4 VMs. A VM running Windows 10 with Splunk forwarding and Sysmon configured on. A VM running Windows Server machine running AD which also had Splunk forwarding and Sysmon configured on. A VM running Ubunutu which was configured for Splunk. Finally a VM running Kali Linux.

## Skills Learned

- Ability to setup ADDS.
- How to setup a SIEM on Ubuntu server.
- Configuring Splunk/Sysmon forwarding from target machines.
- Understanding of generating and reading network logs.
- Start to understand common attacker trends.

## Tools Used

- ViurtalBox for setting up VM enviroment and creating a NAT network.
- ADDS for domain setup and user creating.
- SIEM system for log ingestion and analysis.
- Crowbar to generate brute force attack.
- ART (AtomicRedTeam) to start gaining experience in Mitre Att&ck framework.

## Steps
drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

![adproject-network-diagram](https://github.com/user-attachments/assets/d47fdf38-669e-4452-ab0c-c6fc44962f0e)

Ref 1: Network Diagram

![00-installer-config yaml](https://github.com/user-attachments/assets/9114d4eb-ec00-475f-a53b-b45f239f2cd1)

Ref 2: Splunk network config

![ip -a Splunk](https://github.com/user-attachments/assets/b885d029-8f0e-4871-8ad3-d0dc5f6ff317)

Ref 3: Network config applied

![splunk-login-page](https://github.com/user-attachments/assets/9e32575c-ccff-4008-aa21-ace79b00d572)

Ref 4: Testing Splunk GUI access from client machine

![ADDC Settings](https://github.com/user-attachments/assets/62151b93-3197-4502-9e30-9c8b71e49c81)

Ref 5: AD Local Server Setup

![IT User](https://github.com/user-attachments/assets/eba3b8cd-b971-4558-a000-65e9ec6f6dc7)

Ref 6: IT User

![HR User](https://github.com/user-attachments/assets/87dbcc38-cbb9-40de-a7ba-24fdc04ee66e)

Ref 7: HR User

![inputs conf](https://github.com/user-attachments/assets/86a9d416-9373-4cd6-bd50-fdde22dcbc7c)

Ref 8: Creating new variant of inputs.conf for Splunk index (Client Machine)

![inputs conf location](https://github.com/user-attachments/assets/05440b99-c07d-41f2-861c-64f1bc632237)

Ref 9: New location for inputs.conf

![endpoint-index](https://github.com/user-attachments/assets/407d2de4-fce4-401d-968d-b621dee412b8)

Ref 10: endpoint index created

![receiving-9997](https://github.com/user-attachments/assets/51bbd9ba-8525-47f8-97cf-df6842d00275)

Ref 11: Receiving data port setup

![endpoints-pc-ad](https://github.com/user-attachments/assets/c37888c2-1a91-4ed0-8525-ed6647dc91d8)

Ref 12: Both endpoints showing events

![rdp-win10-client](https://github.com/user-attachments/assets/b075f969-92e6-4db3-a1f0-a6528bda2280)

Ref 13: Enabling RDP on client machine (to help with brute force attack)

![rockyou-passwords-list](https://github.com/user-attachments/assets/e3ff7c98-3b11-4b1f-9125-7f60ec18c081)

Ref 14: Beginning to use Crowbar and generating passwords file for brute force attack

![adding-password](https://github.com/user-attachments/assets/110429e8-2b22-45c3-8716-1bb141de78be)

Ref 15: Example passwords file

![SplunkEventJNeutron](https://github.com/user-attachments/assets/f9597e96-491f-4ded-8cba-c86f5dc38cf9)

Ref 16: Searching specifically for JNeutron user logs

![EventCode4625](https://github.com/user-attachments/assets/a8e3661b-7b7a-4024-8a6a-745bdeadf047)

Ref 17: Event ID referencing failed login attempts

![FailedLoginAttempts](https://github.com/user-attachments/assets/4e902508-2b82-4f3a-b6a9-c760f76d544e)

Ref 18: Telemetry for failed login attempts

![FullEventLogBruteForce](https://github.com/user-attachments/assets/6799dea0-1fa4-4e0a-a882-f4ece2bac066)

Ref 19: Full brute force security log

![InstallingART](https://github.com/user-attachments/assets/f099f10c-9ebd-4ea7-9524-6f6f3c20f92f)

Ref 20: ART

![AtomicTestT1136 001-LocalUser](https://github.com/user-attachments/assets/9505a5c6-e3b3-4255-b4b4-1ffedd728ff1)

Ref 21: ART Persistence 1136.001 creating local account

![DetectingT1136 001-NewLocalUser](https://github.com/user-attachments/assets/49fd45ab-7914-4ecc-b1e5-9c2e1fab6d6f)

Ref 22: Detecting local account creation in Splunk



