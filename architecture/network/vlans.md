# VLAN Architecture (Home Lab)

This document describes the **logical VLAN architecture** and trust boundaries.
Exact addressing and enforcement details are intentionally abstracted or sanitized.

**Environment:** Homelab
**Status:** Reserved (planning stage; enforcement in pfSense + managed switches)  

## VLANs

> **Note:** Subnets shown are representative and may not reflect live addressing.
> Exact IP details are intentionally omitted from public documentation.


| VID | Name        | Subnet         | Role        | Trust Level | Description |
|---:|-------------|----------------|-------------|------------|-------------|
| 10 | MGMT        | 10.227.10.0/24  | Management  | High       | Management plane: Proxmox, NetBox, switch/AP management. Admin access only. |
| 20 | Servers     | 10.227.20.0/24  | SERVERS     | High       | Trusted service tier (Docker services, internal apps). No direct access from IoT/Guest. |
| 25 | IOT-CONTROL | 10.227.25.0/24  | IOT-CONTROL | Medium     | Home Assistant control plane only. Receives IoT traffic; may initiate to Servers for MQTT/DB. |
| 30 | IOT         | 10.227.30.0/24  | IOT         | Low        | Untrusted IoT endpoints (bulbs, plugs, cameras). No lateral access. |
| 40 | USERS       | 10.227.40.0/24  | USERS       | High       | Trusted user devices (PCs/phones). Allowed to HA UI + dashboards; no direct to IoT devices. |
| 50 | GUESTS      | 10.227.50.0/24  | GUESTS      | Lowest     | Guest Wi-Fi. Internet only. |

## Notes
- Inter-VLAN routing is handled by pfSense.
- Default stance: deny inter-VLAN traffic unless explicitly allowed.
- VLAN 25 exists to keep Home Assistant out of the untrusted IoT blast radius.

## Relationship to Firewall Intent Matrix

This VLAN architecture defines **trust zones**, not connectivity.

All inter-VLAN communication is governed by the **Firewall Intent Matrix**, which
documents *allowed traffic based on intent* rather than implicit trust.

- VLANs define **security boundaries**
- The intent matrix defines **permitted flows between boundaries**
- pfSense enforces these rules with a default-deny posture

The VLAN definitions and the firewall intent matrix are designed to be read together:
the VLANs establish *where traffic originates*, and the intent matrix defines *what
that traffic is allowed to do*.
See: [Firewall Intent Matrix](firewall-intent-matrix.md)

## Logical Network Diagram

See the logical network diagram for a visual representation of VLAN
trust boundaries and permitted traffic flows.

➡️ [Logical Network Architecture](network-logical.md)
