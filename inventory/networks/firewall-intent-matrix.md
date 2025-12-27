# Firewall Intent Matrix (Planned)

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
