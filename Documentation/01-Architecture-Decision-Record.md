# Architecture Decision Record (ADR)

## Document Information

| Field | Value |
|--------|-------|
| Project | CyberSOC Home Lab Foundation |
| Version | 1.0 |
| Status | Active |
| Author | Jorge Bayuelo |
| Last Updated | 2026-06-21 |

---

# Purpose

This document captures the architectural decisions made throughout the design and implementation of the CyberSOC Home Lab.

Each Architecture Decision Record (ADR) documents:

- The decision
- The context in which it was made
- The rationale
- Alternatives that were considered
- Consequences of the decision

The purpose of maintaining this document is to provide traceability and explain *why* the lab was designed the way it was.

---

# ADR-001

## Title

Use VMware Workstation Pro as the virtualization platform.

### Status

Accepted

### Context

The CyberSOC Home Lab requires a virtualization platform capable of hosting multiple Windows and Linux virtual machines while supporting advanced networking features such as Host-Only networking, snapshots, virtual TPM, and custom virtual hardware.

### Decision

VMware Workstation Pro 26 will be used as the primary hypervisor.

### Alternatives Considered

- VirtualBox
- KVM/QEMU
- Hyper-V
- Proxmox VE

### Rationale

VMware Workstation Pro provides mature virtualization capabilities, excellent Windows guest support, advanced virtual networking, and snapshot functionality while integrating well with the existing Arch Linux workstation.

### Consequences

The remainder of the lab will be designed around VMware networking and virtual hardware.

---

# ADR-002

## Title

Use a Host-Only virtual network.

### Status

Accepted

### Context

The lab requires isolation from the home network while still allowing communication between the host workstation and all virtual machines.

### Decision

A dedicated Host-Only network (VMnet2) will be created.

### Alternatives Considered

- NAT
- Bridged Networking

### Rationale

Host-Only networking provides a secure environment for attack simulation without exposing lab systems to external networks.

### Consequences

Virtual machines will not have Internet connectivity by default.

Temporary Internet access may be enabled only when required for software installation or updates.

---

# ADR-003

## Title

Disable VMware DHCP.

### Status

Accepted

### Context

The Active Directory environment will eventually provide DHCP services.

### Decision

VMware DHCP will remain disabled.

### Alternatives Considered

- VMware DHCP

### Rationale

Implementing DHCP through Windows Server allows the lab to simulate enterprise Active Directory environments and provides hands-on experience configuring DHCP scopes, reservations, DNS integration, and authorization.

### Consequences

Servers will initially use static IP addresses until DHCP is deployed.

---

# ADR-004

## Title

Use Git Submodules for Portfolio Organization.

### Status

Accepted

### Context

The CyberSOC Portfolio consists of multiple independent projects while also requiring a single portfolio repository that documents the overall program.

### Decision

Each project will be maintained as an independent Git repository and referenced from the CyberSOC Portfolio using Git submodules.

### Alternatives Considered

- Single monolithic repository
- Independent repositories without a master portfolio
- Nested Git repositories

### Rationale

Git submodules preserve independent commit histories while allowing the portfolio repository to serve as a central entry point for documentation, architecture, and project navigation.

### Consequences

Updates to individual projects require commits within both the project repository and the portfolio repository.

---

# ADR-005

## Title

Use an Architecture Decision Record (ADR) methodology.

### Status

Accepted

### Context

Engineering decisions should be documented as they are made rather than reconstructed after project completion.

### Decision

The CyberSOC Portfolio will maintain a living ADR document.

### Alternatives Considered

- No decision log
- Informal documentation in README files

### Rationale

An ADR provides historical context for architectural decisions and improves maintainability, documentation quality, and interview readiness.

### Consequences

All significant architectural decisions throughout the portfolio will be recorded in this document.

---

# Future Decisions

The following decisions will be documented as the project evolves.

- Windows Server Edition
- Firmware (UEFI vs BIOS)
- Secure Boot
- TPM
- VM Hardware Standards
- Active Directory Design
- DNS Architecture
- DHCP Configuration
- Organizational Unit Structure
- Group Policy Design
- SIEM Selection
- Detection Engineering Standards
- Vulnerability Management Workflow
