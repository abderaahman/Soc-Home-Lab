SOC Home Lab
Author: Abdelrahman Magdy Gouda
LinkedIn: LinkedIn Profile

Table of Contents
Introduction
Lab Topology
Attack Scenario Breakdown
Deployment Steps
Windows Deployment
Splunk Deployment
Mythic C2 Deployment
Practical Attack Implementation
Detection and Containment
Lessons Learned
Introduction
This repository contains documentation and resources for a SOC (Security Operations Center) Home Lab built on AWS. The lab simulates a real-world cybersecurity attack and response scenario. The components include:

Windows Server (Victim Machine)
Splunk (SIEM Solution)
Mythic C2 (Command and Control Server)
Kali Linux (Attacker Machine)
This lab walks through the different phases of an attack, including information gathering, gaining access, discovery, payload execution, and data exfiltration, followed by detection and response strategies.

Lab Topology
The lab is deployed on AWS and consists of the following key components:

Kali Linux - Attacker Machine
Mythic C2 Server - Command and Control Server
Splunk - Security Information and Event Management (SIEM) solution
Windows Server 2022 - Victim machine for attacks
Attack Scenario Breakdown
The lab simulates the following phases of a cyberattack:

Information Gathering: The attacker uses Nmap to identify open ports on the victim machine.
Initial Access: Using a brute-force RDP attack to gain access to the Windows Server.
Discovery: Gathering internal system information.
Defense Evasion: Disabling Windows Defender to avoid detection.
Payload Execution: Deploying a backdoor payload.
Command & Control (C2): Maintaining remote control of the victim machine.
Data Exfiltration: Exfiltrating sensitive data from the victim machine.
Deployment Steps
Windows Deployment
This involves creating a VPC, configuring routing tables, and launching EC2 instances for Windows Server, Kali Linux, and Mythic C2. Detailed instructions for setting up AWS services are provided.

Splunk Deployment
Splunk is deployed on an Amazon Linux instance for monitoring and analyzing logs. Instructions include downloading and configuring Splunk, setting up log forwarding, and assigning an Elastic IP for accessibility.

Mythic C2 Deployment
Mythic C2 is deployed on an Ubuntu server for managing the attack payloads and sessions with the compromised victim machine.

Practical Attack Implementation
The attack consists of seven phases:

Information Gathering: Using Nmap to scan for open ports.
Initial Access: Brute-forcing RDP to access the Windows Server.
Discovery: Command-line queries to understand the system environment.
Defense Evasion: Disabling security mechanisms such as Windows Defender.
Payload Execution: Executing malicious payloads using the Mythic C2 server.
Command and Control (C2): Maintaining control over the compromised machine.
Data Exfiltration: Extracting sensitive information from the victim system.
Detection and Containment
The logs collected by Splunk allow detection of the attack. By analyzing Event Code 4776, unusual activity such as failed login attempts and unauthorized processes can be detected. Key containment strategies include isolating the compromised system, terminating C2 connections, blocking the attacker's IP address, and re-enabling security mechanisms like Windows Defender.

Lessons Learned
Key takeaways from the lab include:

Importance of Strong Authentication: Weak RDP passwords made the system vulnerable. Multi-factor authentication (MFA) should be enabled.
Early Detection and Monitoring: Implementing endpoint detection and response (EDR) could have mitigated the attack.
Need for Regular Vulnerability Assessments: Open ports and weak security configurations were exploited. Regular scans should be performed.
Anticipating Defense Evasion Techniques: Security teams must be prepared to detect evasion tactics like disabling antivirus software.
This is a detailed README file that outlines the purpose, components, and steps involved in the SOC Home Lab. You can adjust and add further details as needed based on any specific requirements.
