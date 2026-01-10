# Segmentation Policy

## Scope
This policy applies to all VLAN-based network segmentation
and inter-VLAN traffic within the homelab environment.

## Goals
- Reduce blast radius: compromise of IoT/Guest should not expose Users/Servers/MGMT.
- Keep management interfaces isolated from general client networks.
- Keep rules explainable and maintainable (few clear allows > many exceptions).

## Default Rule
- **Deny** inter-VLAN traffic by default.
- Add **explicit allow** rules only for required flows.

## Enforcement
This policy is enforced centrally at the network firewall.
VLAN membership alone does not imply access between networks.

## High-level allowed flows
- USERS → IOT-CONTROL: Home Assistant UI/dashboards.
- IOT → IOT-CONTROL: device telemetry/control to HA.
- IOT-CONTROL → Servers: only required services (e.g., MQTT/DB/integrations).
- GUESTS → internal networks: **denied** (Internet only).
- MGMT: restricted to admin devices and management endpoints only.

## Related Artifacts
This policy is implemented and reflected in the following documents:

- VLAN architecture and trust boundaries:  
  [/docs/architecture/network/vlans.md](/docs/architecture/network/vlans.md)

- Inter-VLAN traffic intent model:  
  [/docs/architecture/network/firewall-intent-matrix.md](/docs/architecture/network/firewall-intent-matrix.md)

- Architectural decision for segmentation:  
  [/docs/decisions/adr-0001-network-segmentation.md](/docs/decisions/adr-0001-network-segmentation.md)

