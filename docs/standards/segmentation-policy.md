# Segmentation Policy

## Goals
- Reduce blast radius: compromise of IoT/Guest should not expose Users/Servers/MGMT.
- Keep management interfaces isolated from general client networks.
- Keep rules explainable and maintainable (few clear allows > many exceptions).

## Default Rule
- **Deny** inter-VLAN traffic by default.
- Add **explicit allow** rules only for required flows.

## High-level allowed flows
- USERS → IOT-CONTROL: Home Assistant UI/dashboards.
- IOT → IOT-CONTROL: device telemetry/control to HA.
- IOT-CONTROL → Servers: only required services (e.g., MQTT/DB/integrations).
- GUESTS → internal networks: **denied** (Internet only).
- MGMT: restricted to admin devices and management endpoints only.
