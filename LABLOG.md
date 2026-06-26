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
