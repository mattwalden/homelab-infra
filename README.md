# Home Lab Infrastructure (Proxmox + pfSense)

This repository documents my personal home lab used to practice **real-world infrastructure design, network segmentation, and system administration**.  
The focus is on **intentional design**, **security boundaries**, and **clear documentation** rather than shortcuts.

This lab is actively evolving and reflects how I approach planning, implementing, and operating infrastructure.

---

## Core Technologies

- **Proxmox VE** – virtualization platform
- **pfSense** – firewall, inter-VLAN routing, VPN
- **NetBox** – IPAM and source of truth
- **VLAN-segmented network architecture**
- **Linux & Windows Server** workloads
- **Git-based documentation** and change tracking

---

## High-Level Goals

- Design a segmented home network that mirrors enterprise best practices
- Enforce trust boundaries between Users, Servers, IoT, and Guests
- Use documentation as a first-class artifact (not an afterthought)
- Maintain a clear “why” behind architectural and security decisions
- Create a reproducible and explainable lab environment

---

## Network Segmentation Overview

The network is designed around multiple VLANs with a **default-deny inter-VLAN policy** and explicit allow rules based on intent.

### VLAN Highlights
- **MGMT** – Infrastructure management (Proxmox, NetBox, switches)
- **Servers** – Trusted application and service tier
- **IOT-CONTROL** – Home Assistant control plane
- **IOT** – Untrusted IoT devices (bulbs, plugs, cameras)
- **USERS** – Trusted user devices
- **GUESTS** – Internet-only guest access

📄 Detailed VLAN inventory:  
➡️ [`inventory/networks/vlans.md`](inventory/networks/vlans.md)

📄 Segmentation design principles:  
➡️ [`docs/standards/segmentation-policy.md`](docs/standards/segmentation-policy.md)

📄 Planned firewall intent matrix:  
➡️ [`inventory/networks/firewall-intent-matrix.md`](inventory/networks/firewall-intent-matrix.md)

---

## Design Philosophy

- **Plan before implementing** (VLANs, firewall rules, IPAM first)
- **Default deny, explicit allow**
- **Separate control planes from untrusted devices**
- **Document decisions and tradeoffs**
- **Treat a home lab like a production environment**

---

## Repository Structure (Highlights)


