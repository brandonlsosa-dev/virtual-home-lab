# Virtual Home Lab

A fully documented home lab environment built with VMware Workstation Pro, simulating enterprise IT infrastructure including Active Directory, DNS, DHCP, Linux services, and a virtual firewall. Built as a hands-on learning project to develop real-world System Administration skills.

---

## Overview

This lab replicates the core infrastructure found in small-to-medium business environments. All machines run inside VMware Workstation Pro using isolated virtual networks routed through a pfSense firewall.

**Technologies used:** VMware Workstation Pro · Windows Server 2022 · Ubuntu Server 22.04 · pfSense · Active Directory · DNS · DHCP · Apache · Samba · SSH

---

## Network topology

```
Internet / NAT (VMnet8 · 192.168.0.0/24)
        |
   pfSense Firewall
   /         |          \
Server LAN  Client LAN  Management
10.0/24     20.0/24     30.0/24
```

| Subnet         | Network           | CIDR              | Purpose                        |
|----------------|-------------------|-------------------|--------------------------------|
| WAN            | VMware NAT/VMnet8 | 192.168.0.0/24    | pfSense internet uplink        |
| Server LAN     | VMnet2 host-only  | 192.168.10.0/24   | Domain controller + Ubuntu     |
| Client LAN     | VMnet3 host-only  | 192.168.20.0/24   | Windows 10 workstation         |
| Management     | VMnet4 host-only  | 192.168.30.0/24   | Admin SSH / RDP access         |

---

## Virtual machines

| VM                  | OS                    | IP             | Roles                              |
|---------------------|-----------------------|----------------|------------------------------------|
| DC01                | Windows Server 2022   | 192.168.10.10  | AD DS, DNS, DHCP                   |
| UBUNTU-SRV01        | Ubuntu Server 22.04   | 192.168.10.20  | Apache, Samba, SSH                 |
| WIN10-CLIENT01      | Windows 10 Pro        | DHCP / .20.50  | Domain-joined workstation          |
| PFSENSE-FW01        | pfSense 2.7           | Multi-homed    | Firewall, routing, NAT             |

---

## Lab environment

| Item              | Detail                              |
|-------------------|-------------------------------------|
| Host OS           | *(your OS here)*                    |
| CPU               | *(your CPU here)* — VT-x enabled    |
| RAM               | *(your RAM here)*                   |
| Disk              | *(your available disk here)*        |
| Hypervisor        | VMware Workstation Pro *(version)*  |

---

## Project phases

- [x] Phase 1 — Hypervisor setup
- [x] Phase 2 — Virtual network design
- [ ] Phase 3 — ISO downloads and VM creation
- [ ] Phase 4 — pfSense firewall configuration
- [ ] Phase 5 — Windows Server: AD DS, DNS, DHCP
- [ ] Phase 6 — Ubuntu Server: Apache, Samba, SSH
- [ ] Phase 7 — Domain join and Group Policy
- [ ] Phase 8 — Testing and verification

---

## Key learning outcomes

- Virtualization and multi-VM networking
- Windows Server configuration (Active Directory, DNS, DHCP)
- Linux server setup and service deployment
- Firewall configuration and inter-subnet routing
- Domain join, Group Policy, and troubleshooting

---

## Documentation

Full build documentation is in [`/docs`](./docs):

- [`network-design.md`](./docs/network-design.md) — IP addressing, subnet decisions, topology
- [`windows-server.md`](./docs/windows-server.md) — AD DS setup, DNS zones, DHCP scopes
- [`ubuntu-server.md`](./docs/ubuntu-server.md) — Apache, Samba, SSH configuration
- [`pfsense.md`](./docs/pfsense.md) — Firewall rules, NAT, routing
- [`troubleshooting.md`](./docs/troubleshooting.md) — Issues encountered and how they were resolved

---

## Status

Currently in progress. Phases 1–2 complete.
