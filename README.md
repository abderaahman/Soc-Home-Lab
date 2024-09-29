
# SOC Home Lab

**Author**: Abdelrahman Magdy Gouda  
**LinkedIn**: [LinkedIn Profile](https://www.linkedin.com/in/abdelrahman-magdyy/)

---

## Overview

This repository contains documentation and resources for a Security Operations Center (SOC) home lab deployed on AWS. The lab is designed to simulate real-world cyberattack scenarios and demonstrate how to detect, mitigate, and respond to security incidents. It includes a victim machine, attacker machine, Command and Control (C2) server, and a Security Information and Event Management (SIEM) solution for monitoring and analysis.

Key components:
- Windows Server – Target victim machine
- Splunk – SIEM solution for log analysis and incident detection
- Mythic C2 – Command and Control server for managing attacks
- Kali Linux – Attacker machine used for penetration testing and exploitation

This lab simulates the lifecycle of an attack, from reconnaissance and exploitation to data exfiltration, along with defense mechanisms and containment strategies.

---

## Lab Topology

The lab is deployed within an AWS infrastructure, consisting of the following components:
- Kali Linux – Attacker machine used for reconnaissance and exploitation
- Mythic C2 – Command and Control (C2) server used to deploy and manage payloads
- Splunk – SIEM platform for real-time monitoring and log analysis
- Windows Server 2022 – Victim machine vulnerable to attacks

Each of these components is hosted on AWS EC2 instances, interconnected within a Virtual Private Cloud (VPC) environment.

---

## Attack Scenario Breakdown

The attack simulation is broken down into seven distinct phases:

- **Information Gathering**: Using tools like Nmap, the attacker scans for open ports and vulnerable services on the target machine.
- **Initial Access**: A brute-force attack is executed on the Remote Desktop Protocol (RDP) service of the Windows Server to gain unauthorized access.
- **Discovery**: Once inside, the attacker gathers critical system information such as users, network configuration, and services.
- **Defense Evasion**: The attacker disables Windows Defender to avoid detection and ensure continued access.
- **Payload Execution**: A backdoor payload is deployed on the victim machine to establish persistent access.
- **Command & Control (C2)**: The attacker maintains remote control over the compromised server using Mythic C2.
- **Data Exfiltration**: Sensitive data is extracted from the victim server to the attacker's C2 infrastructure.

---

## Deployment Steps

### Windows Deployment
- **VPC Creation**: Set up a dedicated Virtual Private Cloud (VPC) in AWS to host the lab infrastructure.
- **EC2 Instances**: Deploy Windows Server 2022, Kali Linux, Splunk, and Mythic C2 as separate EC2 instances, each with its own security group and networking configuration.
- **Network Configuration**: Create routing tables, subnets, and internet gateways to ensure proper connectivity between the machines.

### Splunk Deployment
- **Instance Setup**: Install Splunk on an Amazon Linux EC2 instance.
- **Log Forwarding**: Configure the Splunk Forwarder on the Windows Server to forward logs to the Splunk instance for real-time monitoring.
- **Security Configuration**: Set up security rules to allow access to Splunk over port 8000.

### Mythic C2 Deployment
- **Ubuntu Setup**: Deploy Mythic C2 on an Ubuntu server in a separate VPC from the other instances to simulate an external attacker.
- **Payload Creation**: Configure and deploy payloads using Mythic C2 to target the Windows Server.
- **C2 Session Management**: Manage and control compromised machines using Mythic's C2 functionality.

---

## Practical Attack Implementation

This lab covers a hands-on approach to simulating a full attack lifecycle. It includes:
- **Phase 1: Information Gathering**: Using Nmap to scan for open ports, such as RDP on the victim machine.
- **Phase 2: Initial Access**: Gaining access to the Windows Server through brute-force attacks on the RDP service using tools like Crowbar.
- **Phase 3: Discovery**: Identifying critical system information using commands like `whoami`, `net user`, and `ipconfig`.
- **Phase 4: Defense Evasion**: Disabling security tools like Windows Defender to remain undetected.
- **Phase 5: Payload Execution**: Executing a malicious payload using Mythic C2 to establish persistent access.
- **Phase 6: Command & Control**: Maintaining remote control over the victim through Mythic C2 sessions.
- **Phase 7: Data Exfiltration**: Exfiltrating sensitive files, such as password files, from the victim machine.

---

## Detection and Containment

### Detection
Using Splunk, the attack is detected by monitoring logs for unusual events, such as:
- Repeated login failures (Event Code 4776)
- Unauthorized process execution (e.g., custom malicious processes)
- New user accounts created by the attacker

### Containment
To contain the attack and prevent further damage:
- **Isolate the Victim**: Disconnect the compromised Windows Server from the network.
- **Terminate C2 Sessions**: Block the C2 connections to cut off the attacker's access.
- **Firewall Adjustments**: Block the attacker's IP and update firewall rules to prevent future attacks.
- **Remove Unauthorized Users**: Remove any accounts created by the attacker and re-enable security measures like Windows Defender.

---

## Lessons Learned

- **Importance of Strong Authentication**: Weak passwords allowed brute-force attacks to succeed. Implementing multi-factor authentication (MFA) would prevent such attacks.
   
- **Early Detection and Monitoring**: Endpoint detection and response (EDR) solutions should be deployed to detect and respond to malicious activities like disabling security services or abnormal RDP sessions.

- **Regular Vulnerability Assessments**: Open ports, especially services like RDP, should be routinely scanned and secured to prevent exploitation.

- **Anticipating Defense Evasion**: Attackers often disable security measures. Continuous monitoring and integrity checks should be performed to detect such evasion techniques.

---

## Conclusion

This SOC Home Lab provides a comprehensive, hands-on experience of simulating and detecting cyberattacks in a controlled environment. It serves as a valuable resource for learning about attack methods, detection strategies, and incident response techniques.

---
