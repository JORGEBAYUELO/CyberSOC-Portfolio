# LABLOG

## 2026-06-21

### Project 0 – CyberSOC Home Lab Foundation

**Phase 1 – Lab Infrastructure**

**Status:** Completed

#### Accomplishments

* Designed the architecture for the CyberSOC Home Lab.
* Created the CyberSOC Portfolio repository and project structure.
* Configured Git submodules for independent project version control.
* Created the VMware Host-Only network (VMnet2).
* Disabled VMware DHCP to allow Windows Server to manage addressing later in the project.
* Established the documentation and repository structure for the portfolio.

#### Environment

* Host OS: Arch Linux
* Hypervisor: VMware Workstation Pro 26
* Virtual Network: VMnet2 (Host-Only)
* Subnet: 192.168.100.0/24

#### Evidence

* Screenshot 001 – VMware Network Configuration

#### Next

Build the first virtual machine (`CYBER-DC01`) and install Windows Server 2022.

---

## 2026-06-21

### Phase 2 – Domain Controller Deployment

**Status:** Completed

#### Accomplishments

* Created the `CYBER-DC01` virtual machine.
* Configured UEFI firmware with Secure Boot enabled.
* Allocated 4 vCPUs, 6 GB RAM, and an 80 GB thin-provisioned NVMe virtual disk.
* Installed Windows Server 2022.
* Installed VMware Tools.
* Renamed the server to `CYBER-DC01`.
* Configured a static IPv4 address (`192.168.100.10`).
* Applied the latest Windows updates before promoting the server.
* Installed the Active Directory Domain Services role.
* Promoted the server to the first Domain Controller.
* Created the `cybersoc.lab` Active Directory forest and domain.
* Installed and configured the DNS Server role.
* Validated the Domain Controller using `dcdiag /v`.
* Verified DNS registration and SYSVOL replication.

#### Environment

* Hostname: `CYBER-DC01`
* Domain: `cybersoc.lab`
* IP Address: `192.168.100.10`
* DNS Server: `192.168.100.10`

#### Evidence

* Screenshot 002 – Windows Server Installation
* Screenshot 003 – Initial Server Configuration
* Screenshot 004 – Domain Controller Promotion
* Screenshot 005 – Server Manager After Promotion

#### Next

Design the Active Directory organizational structure.

---

## 2026-06-22

### Phase 3 – Active Directory Organization

**Status:** Completed

#### Accomplishments

* Designed and implemented the Active Directory Organizational Unit (OU) hierarchy.
* Created dedicated OUs for administrative accounts, servers, workstations, user accounts, and security groups.
* Preserved the default `Domain Controllers` OU for Domain Controllers.
* Created administrative user accounts for privileged administration.
* Created standard user accounts across multiple departments.
* Created Global Security Groups for departmental access control.
* Assigned users to the appropriate security groups.
* Established a realistic Active Directory environment that will support future authentication, Group Policy, detection engineering, vulnerability management, and attack simulation exercises.

#### Organizational Units

**Admin**

* Domain Admins
* Server Admins
* Service Accounts

**Servers**

* Infrastructure
* SIEM

**User Accounts**

* IT
* HR
* Finance
* Marketing

**Workstations**

* IT
* HR
* Finance
* Marketing

**Groups**

* Security
* Distribution

#### Security Groups

* GG_IT_Users
* GG_HR_Users
* GG_Finance_Users
* GG_Marketing_Users
* GG_Server_Admins
* GG_Helpdesk
* GG_SIEM_Admins

#### Administrative Accounts

* adm.jbayuelo
* srv.jbayuelo

#### Evidence

* Screenshot 006 – Organizational Unit Structure
* Screenshot 007 – User Accounts
* Screenshot 008 – Security Groups
* Screenshot 009 – Group Memberships

#### Next

Deploy the first Windows 11 Enterprise workstation, join it to the `cybersoc.lab` domain, and begin building the client environment for endpoint management, security monitoring, and attack simulation.

## 2026-06-26

### Phase 4 – Windows 11 Enterprise Client Deployment

#### Objective

Deploy the first Windows 11 Enterprise workstation that will be joined to the CyberSOC Active Directory domain.

#### Accomplishments

- Created the WIN11-CLIENT01 virtual machine in VMware Workstation.
- Configured the VM with:
  - UEFI firmware
  - Secure Boot
  - Virtual TPM
  - VMnet2 private network
- Installed Windows 11 Enterprise.
- Completed the initial operating system setup.
- Installed VMware Tools.
- Verified proper display scaling and improved VM integration.
- Captured a baseline screenshot after installation.

#### Result

The Windows 11 Enterprise client is successfully deployed and ready for domain integration.

### Phase 5 – Group Policy Foundation

#### Objective

Establish the initial Group Policy infrastructure for domain joined workstations and verify successful policy application.

#### Tasks Completed

* Moved **WIN11-CLIENT01** from the default **Computers** container into the **Workstations** Organizational Unit.
* Created and linked the **Corporate Workstation Baseline** Group Policy Object to the **Workstations** OU.
* Configured the initial Microsoft Defender Antivirus baseline settings within the GPO.
* Forced a Group Policy update on **WIN11-CLIENT01** using:

```
gpupdate /force
```

* Verified successful Group Policy application using:

```
gpresult /r
```

#### Validation

Verified the following:

* Corporate Workstation Baseline appears under **Applied Group Policy Objects**.
* Default Domain Policy is successfully applied.
* The client receives Group Policy from **CYBER-DC01.cybersoc.lab**.
* The workstation is authenticated to the **CYBERSOC** domain.
* Group Policy processing completed without errors.

#### Outcome

The Active Directory environment now includes a centralized Group Policy management framework. Workstations receive security configurations through domain policies, providing the foundation for future hardening, logging, auditing, Sysmon deployment, Windows Event Forwarding, and SIEM integration.

#### Evidence

Screenshot:

* `07_Corporate_Workstation_Baseline_Applied.png`

### Phase 6 – Endpoint Telemetry with Sysmon

Completed the deployment of Microsoft Sysmon on WIN11-CLIENT01 to improve endpoint visibility beyond native Windows Security logs.

#### Accomplishments:

- Created the Sysmon tools directory on the Windows 11 client.
- Downloaded and extracted the Sysinternals Sysmon package.
- Downloaded the SwiftOnSecurity Sysmon configuration.
- Installed Sysmon using the custom XML configuration.
- Verified the Sysmon service and driver were successfully installed.
- Generated process creation events by launching test applications.
- Verified Event ID 1 (Process Creation) entries in the Sysmon Operational log.
- Confirmed detailed telemetry including Process GUIDs, command lines, SHA256 hashes, integrity levels, parent processes, and user context.

#### Outcome:

The Windows 11 workstation is now producing enterprise-grade endpoint telemetry that will later be forwarded to the centralized logging infrastructure and SIEM.

## 2026-06-28

### Validate Windows Event Forwarding Infrastructure

#### Objective

Verify that Windows Event Forwarding (WEF) successfully forwards events from a domain-joined workstation to the Domain Controller.

#### Tasks Completed

- Modified the WEF subscription to collect System log events.
- Restarted the Windows 11 client to generate test events.
- Confirmed that forwarded events appeared in the Forwarded Events log on CYBER-DC01.
- Verified the source computer was correctly identified as WIN11-CLIENT01.cybersoc.lab.
- Confirmed successful communication between the Event Collector and the workstation.

#### Key Findings

- The Windows Event Forwarding infrastructure is fully operational.
- WinRM, GPO configuration, Subscription Manager, and Event Collector services are functioning correctly.
- The previous issue was isolated specifically to forwarding Security log events rather than the WEF infrastructure itself.

#### Skills Demonstrated

- Windows Event Forwarding (WEF)
- Event Collector configuration
- WinRM configuration
- Group Policy management
- Windows Event Viewer
- Infrastructure validation
- Enterprise troubleshooting methodology
