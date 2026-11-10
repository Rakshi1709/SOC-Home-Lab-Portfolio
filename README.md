# SOC Home Lab — Windows Security Monitoring & Incident Investigation

## 1. Project Overview

This project demonstrates the implementation of an isolated Security Operations Center (SOC) home lab using Wazuh SIEM, Windows endpoints, Active Directory, and Kali Linux.

The objective was to configure endpoint security monitoring, collect Windows security events, investigate authentication activity, and perform basic network reconnaissance in a controlled environment.

## 2. Lab Architecture

| Component | Configuration | Purpose |
|---|---|---|
| Wazuh Manager | Ubuntu 22.04 — 192.168.205.132 | Security event collection and analysis |
| Active Directory Domain Controller | Windows Server 2025 — 192.168.205.135 | Domain authentication and DNS |
| Windows Client | Windows 11 Pro — 192.168.205.136 | Endpoint security event generation |
| Attacker Machine | Kali Linux — 192.168.205.133 | Controlled network reconnaissance |
| SIEM Dashboard | Wazuh Dashboard | Security event monitoring and investigation |
| Virtual Network | VMware VMnet1 Host-only — 192.168.205.0/24 | Isolated lab communication |

**Active Directory Domain:** corp.local

**Domain Controller:** AD-DC

## 3. Technologies Used

- Wazuh SIEM
- Ubuntu Linux
- Windows Server 2025
- Windows 11 Pro
- Active Directory Domain Services (AD DS)
- Kali Linux
- VMware Workstation Pro
- Nmap
- Wireshark

## 4. Implementation

### 4.1 Infrastructure Setup

- Created an isolated VMware Host-only network.
- Deployed Ubuntu as the Wazuh Manager.
- Configured Windows Server as an Active Directory Domain Controller.
- Created organizational units, security groups, and test accounts.
- Joined the Windows 11 client to the corp.local domain.

### 4.2 Wazuh Agent Configuration

- Installed the Wazuh agent on the Windows 11 endpoint.
- Configured the agent to communicate with the Wazuh Manager.
- Verified agent connectivity and Windows event collection.
- Monitored endpoint telemetry through the Wazuh Dashboard.

### 4.3 Security Event Investigation

- Generated controlled Windows authentication activity.
- Investigated failed and successful logon events.
- Examined event fields and associated Wazuh alerts.
- Reviewed Ubuntu administrative activity.

### 4.4 Network Reconnaissance

- Performed TCP connect scanning from Kali Linux against the Windows endpoint.
- Used Wireshark to inspect TCP connection attempts and responses.
- Examined observed port responses and packet-level activity.

## 5. Validation Results

| Activity | Evidence | Result |
|---|---|---|
| Failed Windows logon | Event ID 4625; Wazuh Rule 60122 | Confirmed |
| Successful Windows logon | Event ID 4624 | Confirmed |
| Ubuntu sudo activity | Wazuh sudo alert | Confirmed |
| Windows agent connectivity | Agent 002 connected | Confirmed |
| Windows event collection | Windows events visible in Wazuh | Confirmed |
| Kali TCP reconnaissance | Nmap results | Confirmed |
| Packet-level investigation | Wireshark capture | Confirmed |
| Nmap-specific Wazuh alert | No scan-specific alert demonstrated | Not confirmed |

## 6. Detection Limitation

Although the Nmap scan and corresponding TCP traffic were observed, a scan-specific Wazuh alert was not demonstrated.

This highlights the distinction between endpoint telemetry collection, network traffic visibility, and security detection.

Potential improvements include integrating network intrusion detection capabilities such as Suricata or collecting Windows Firewall logs with appropriate detection rules.

## 7. Project Scope

This is an educational SOC home lab, not a production SOC deployment.

The project demonstrates foundational skills in:

- SIEM deployment and configuration
- Windows endpoint monitoring
- Active Directory administration
- Authentication-event investigation
- Basic network reconnaissance
- Packet analysis
- Security-event interpretation
- Technical documentation

The results are limited to the activities explicitly tested in this environment.

## 8. Repository Structure

```text
SOC_homelab_portfolio/
├── lab_setup/
│   └── AD_SOC_lab_Architecture.docx
├── agent_connectivity/
├── Detection_Evidence/
├── Incident_Reports/
│   ├── IR_001_Failed_windows_logon.docx
│   └── IR-002_Successful_windows_logon.docx
└── README.md