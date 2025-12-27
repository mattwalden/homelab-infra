# VLAN Inventory (Home Lab)

**Tenant:** Homelab  
**Status:** Reserved (planning stage; enforcement in pfSense + managed switches)  

## VLANs

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
