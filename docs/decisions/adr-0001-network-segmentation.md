# ADR-0001: VLAN-Based Network Segmentation with Centralized Firewalling

**Status:** Accepted  
**Date:** 2025-12-27  

## Context
The home lab hosts a mix of infrastructure management systems, user devices, servers, IoT devices, and guest clients.  
A flat network would allow unnecessary lateral movement and increase the blast radius of a compromised device, particularly from untrusted IoT endpoints.

The lab also needs:
- Clear trust boundaries
- Centralized enforcement of security policy
- Simple, auditable routing and firewall behavior
- Compatibility with consumer and prosumer network hardware

## Decision
Implement **VLAN-based network segmentation**, with **pfSense acting as the single point of inter-VLAN routing and firewall enforcement**.

Each VLAN represents a distinct trust zone (MGMT, Servers, IOT-CONTROL, IOT, USERS, GUESTS).  
All inter-VLAN traffic is denied by default and explicitly allowed only where required.

## Rationale
- VLANs provide strong logical separation without requiring separate physical networks
- Centralized routing simplifies troubleshooting and auditing
- pfSense offers mature firewalling, alias management, logging, and VPN support
- This model mirrors common enterprise “router-on-a-stick” or firewall-core designs

## Alternatives Considered
### Flat Network
- Rejected due to lack of isolation and high blast radius

### Layer-3 Switch Routing
- Rejected to avoid duplicating security policy across devices
- Central firewall provides clearer visibility and control

## Consequences
### Positive
- Reduced lateral movement risk
- Clear security boundaries
- Predictable traffic flows
- Easier documentation and troubleshooting

### Negative
- Increased firewall rule complexity
- Initial setup requires more planning
- Slight performance overhead compared to pure L3 switching (acceptable for lab scale)

## Notes
This decision intentionally favors **clarity and security over convenience**.

## Related Artifacts

This decision is implemented and reflected in the following documentation:

- VLAN architecture and trust boundaries:  
  `docs/architecture/network/vlans.md`

- Inter-VLAN traffic intent and policy model:  
  `docs/architecture/network/firewall-intent-matrix.md`

These documents describe how the segmentation model defined in this ADR
is expressed in the logical network design and enforced in practice.

**Review cadence:** As-needed (network architecture changes)  

