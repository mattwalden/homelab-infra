# Home Lab Infrastructure (Proxmox + pfSense)

This repository documents my personal home lab used to practice **real-world infrastructure design, network segmentation, and system administration**.

The focus is on **intentional design**, **security boundaries**, and **clear documentation** rather than shortcuts or ad-hoc experimentation.

This lab is actively evolving and reflects how I plan, implement, and operate infrastructure.

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

The network is designed around multiple VLANs with a **default-deny inter-VLAN policy**, with explicit allow rules based on documented intent.
📄 Network architecture overview:  
➡️ [`architecture/network/`](architecture/network/)



### VLAN Highlights
- **MGMT** – Infrastructure management (Proxmox, NetBox, switches)
- **Servers** – Trusted application and service tier
- **IOT-CONTROL** – Home Assistant control plane
- **IOT** – Untrusted IoT devices (bulbs, plugs, cameras)
- **USERS** – Trusted user devices
- **GUESTS** – Internet-only guest access

📄 VLAN design and purpose:  
➡️ [`docs/architecture/network/vlans.md`](docs/architecture/network/vlans.md)

📄 Segmentation standards and policy:  
➡️ [`docs/standards/segmentation-policy.md`](docs/standards/segmentation-policy.md)

📄 Firewall intent matrix (sanitized):  
➡️ [`docs/architecture/network/firewall-intent-matrix.md`](docs/architecture/network/firewall-intent-matrix.md)

---

## Design Philosophy

- **Plan before implementing** (VLANs, firewall rules, IPAM first)
- **Default deny, explicit allow**
- **Separate control planes from untrusted devices**
- **Document decisions and tradeoffs**
- **Treat a home lab like a production environment**

---

## Repository Structure (Highlights)

This repository is intentionally structured to separate *why*, *rules*, and *design*:

- **`docs/decisions/`**  
  Architecture Decision Records (ADRs) explaining *why* key design choices were made.

- **`docs/standards/`**  
  Policies and standards that guide how infrastructure is designed and configured.

- **`docs/architecture/`**  
  High-level, sanitized descriptions of the lab’s structure (network segmentation, trust zones, service placement).

> Note: Exact IP addresses, credentials, firewall configurations, and live system details are intentionally excluded.
