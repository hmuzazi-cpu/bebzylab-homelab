# Wazuh SIEM Lab

## Overview
This project documents the deployment of a Wazuh SIEM (Security Information and Event Management) 
lab built on a Late 2015 iMac using UTM virtualisation. The lab simulates a real SOC monitoring 
environment with a dedicated Wazuh server monitoring two Windows endpoints — a Windows Server 2022 
Active Directory domain controller and a Windows 10 Pro client machine.

This project builds directly on my Active Directory home lab (bebzylab.local) and demonstrates 
skills in SIEM deployment, agent configuration, security event monitoring, and threat detection 
aligned to the MITRE ATT&CK framework.

## Lab Architecture

| Component | OS | IP Address | Role |
|-----------|-----|------------|------|
| wazuh-server | Ubuntu 22.04 LTS | 192.168.64.4 | Wazuh Manager, Indexer, Dashboard |
| bebzylab-dc | Windows Server 2022 | 192.168.64.10 | Active Directory Domain Controller |
| bebzylab-win10 | Windows 10 Pro | 192.168.64.20 | Domain joined endpoint |

All VMs run on UTM on a Late 2015 iMac via a shared internal network (192.168.64.0/24).

## Tools and Technologies
- Wazuh 4.7.5 (Manager, Indexer, Dashboard)
- Ubuntu Server 22.04 LTS
- Windows Server 2022 (Active Directory)
- Windows 10 Pro
- UTM Hypervisor (macOS)
- MITRE ATT&CK Framework

## Project Phases

### Phase 1 — Ubuntu Server VM
Deployed Ubuntu Server 22.04 LTS as a VM in UTM with 4 vCPU, 8GB RAM, and 80GB disk.
Configured networking on the shared 192.168.64.0/24 subnet and confirmed internet connectivity.

![Ubuntu VM IP](screenshots/01-ubuntu-vm-ip.png)

### Phase 2 — Wazuh Installation
Deployed Wazuh 4.7.5 using the official all-in-one install script. The script automatically 
installed and configured the Wazuh Manager, Wazuh Indexer, Filebeat, and Wazuh Dashboard.

![Wazuh Install Complete](screenshots/02-wazuh-install-complete.png)
![Wazuh Login Screen](screenshots/03-wazuh-login-screen.png)
![Wazuh Dashboard](screenshots/04-wazuh-dashboard.png)

### Phase 3 — Agent Deployment
Installed the Wazuh agent on both Windows VMs using PowerShell. Both agents registered 
successfully and reported as active in the dashboard within seconds.

![Agents Connected](screenshots/05-agents-connected.png)
![Wazuh Service Started](screenshots/wazuh-service-started...ccessfully.png)

### Phase 4 — Security Event Generation
Generated and captured three categories of real security events:

#### Brute Force Simulation — Rule 60122
Simulated a brute force attack by entering incorrect passwords multiple times on the 
Windows 10 VM. Wazuh detected every failed attempt mapped to MITRE techniques T1078 
(Valid Accounts) and T1531 (Account Access Removal) with Level 5 severity.

![Failed Login Alerts](screenshots/failed-login-security...0-60122.png)

#### Active Directory User Creation — Rule 60109
Created a new AD user account (HackedUser) via PowerShell on the domain controller. 
Wazuh detected the account creation and changes mapped to MITRE T1098 (Account Manipulation) 
with Level 8 severity under the Persistence tactic.

![User Account Created](screenshots/user-account-created...d-60109.png)
![User Account Changed](screenshots/user-account-created...9-60110.png)

#### File Integrity Monitoring — Rule 554
Enabled real-time FIM on the Windows 10 Desktop directory via ossec.conf. Created a 
test file (secret-passwords.txt) and Wazuh immediately detected the file creation 
with Level 5 severity under Rule 554.

![FIM Alert](screenshots/file-integrity-manage...lert-554.png)

## Key Skills Demonstrated
- SIEM deployment and configuration (Wazuh)
- Security agent deployment across Windows endpoints
- Windows event log monitoring and analysis
- Active Directory security monitoring
- File Integrity Monitoring (FIM) configuration
- MITRE ATT&CK framework mapping
- Brute force and account manipulation detection
- Linux server administration (Ubuntu)
- Network configuration across virtualised environments

## Certifications
- CompTIA A+
- CompTIA Security+
- CompTIA Network+
- AZ-900 (in progress)

## Related Projects
- [Active Directory Home Lab](../active-directory-lab/README.md)

## GitHub
[github.com/hmuzazi-cpu/bebzylab-homelab](https://github.com/hmuzazi-cpu/bebzylab-homelab)