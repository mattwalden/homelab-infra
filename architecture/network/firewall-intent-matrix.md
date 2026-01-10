# Firewall Intent Matrix (Planned)
## Purpose

This matrix defines **allowed traffic intent** between VLAN trust zones.
It is designed to be read alongside the VLAN architecture document and
serves as the basis for firewall rule implementation.

Legend:
- ✅ Allowed (explicit rule)
- ❌ Denied (default block)
- ⚠️ Conditional (restricted by host + port aliases)

| Source \ Destination | MGMT | Servers | IOT-CONTROL | IOT | USERS | GUESTS | Internet |
|---|---:|---:|---:|---:|---:|---:|---:|
| MGMT        | — | ⚠️ | ⚠️ | ❌ | ❌ | ❌ | ✅ |
| Servers     | ⚠️ | — | ⚠️ | ❌ | ⚠️ | ❌ | ✅ |
| IOT-CONTROL | ⚠️ | ⚠️ | — | ⚠️ | ⚠️ | ❌ | ✅ |
| IOT         | ❌ | ❌ | ✅ | — | ❌ | ❌ | ✅ |
| USERS       | ❌ | ⚠️ | ✅ | ❌ | — | ❌ | ✅ |
| GUESTS      | ❌ | ❌ | ❌ | ❌ | ❌ | — | ✅ |

## Notes
- “⚠️ Conditional” = limited to defined aliases (hosts + ports), not blanket access.
- Logging should be enabled on default-deny inter-VLAN blocks during rollout.

> This matrix is visualized in the logical network diagram.  
> See: [Logical Network Architecture](/docs/diagrams/network-logical.md)


