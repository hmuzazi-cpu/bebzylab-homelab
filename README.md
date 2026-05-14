# BebzyLab — Active Directory Home Lab

## Overview
A fully functional Windows Server 2022 Active Directory home lab built from scratch on macOS using UTM virtualisation. This project demonstrates practical IT infrastructure skills across domain configuration, identity and access management, Group Policy, and security monitoring.

**Environment:**
- Host: iMac (macOS Sequoia) running UTM
- Domain Controller: Windows Server 2022 Standard (Desktop Experience)
- Client Machine: Windows 10 Pro
- Domain: bebzylab.local

---

## Phase 1 — Foundation

**Objectives:** Build the core infrastructure from scratch.

**What I did:**
- Installed and configured Windows Server 2022 in UTM
- Promoted the server to a Domain Controller for `bebzylab.local`
- Configured DNS (pointing to DC at 192.168.100.10) and DHCP (scope 192.168.100.50–150)
- Joined a Windows 10 Pro client to the domain
- Created and linked a GPO (`Lab-Baseline-Policy`) and verified it applied to the client using `gpresult /r`

**Key concepts demonstrated:**
- AD DS installation and domain promotion
- DNS dependency for domain joining
- DHCP scope configuration and authorisation in AD
- Group Policy application and verification

---

## Phase 2 — Identity & Access Management

**Objectives:** Build a realistic user and access structure and simulate helpdesk scenarios.

**What I did:**
- Created four Organisational Units: IT, HR, Finance, Helpdesk
- Created 6 domain user accounts across the OUs (jsmith, sconnor, eclarke, mwebb, tbriggs, lpatel)
- Created security groups for each department and added users as members
- Configured account lockout policy via Default Domain Policy (5 attempts, 30 minute lockout)
- Simulated three helpdesk tickets:
  - **Ticket 1:** Triggered and resolved an account lockout for jsmith
  - **Ticket 2:** Performed a password reset for eclarke with forced change at next logon
  - **Ticket 3:** Onboarded a new starter (jtaylor) into the HR OU and HR-Staff security group

**Key concepts demonstrated:**
- OU design and user lifecycle management
- Security group membership and RBAC principles
- Account lockout policy configuration
- Real-world helpdesk procedures

---

## Phase 3 — Security & Monitoring

**Objectives:** Enable security auditing and simulate and investigate a threat.

**What I did:**
- Enabled audit policies via GPO (account logon events, logon events, account management, policy change) — all set to Success and Failure
- Simulated a brute force attack against jsmith from the client machine
- Investigated the attack using Windows Event Viewer:
  - **Event ID 4625** — Failed logon attempts captured on the client
  - **Event ID 4740** — Account lockout event on the DC, confirming jsmith was locked out from BEBZY-CLIENT001
- Created an inbound Windows Firewall rule to block ICMP (ping), verified it blocked traffic from the client, then disabled it

**Key concepts demonstrated:**
- Audit policy configuration via GPO
- Security event log analysis (Event IDs 4625, 4740)
- Identifying brute force patterns in logs
- Windows Defender Firewall rule creation and management

---

## Skills Demonstrated
- Windows Server 2022 administration
- Active Directory DS — domain setup, OUs, users, groups
- Group Policy — creation, linking, enforcement, troubleshooting
- DNS and DHCP configuration
- Network troubleshooting (static IP, subnet, ping, ipconfig)
- Security monitoring and event log analysis
- Helpdesk procedures — password resets, account unlocks, new starter onboarding
- Virtualisation — UTM on macOS

## Certifications
- CompTIA A+ ✓
- CompTIA Security+ ✓
- CompTIA Network+ ✓
- Microsoft AZ-900 (in progress)
