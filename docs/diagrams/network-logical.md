# Logical Network Architecture

This diagram represents the **logical network segmentation** and
**inter-VLAN traffic intent**. It is intentionally sanitized and
does not reflect physical topology or exact addressing.

```mermaid
flowchart LR
    %% Zones
    MGMT[MGMT VLAN<br/>(Management)]
    SERVERS[Servers VLAN<br/>(Trusted Services)]
    USERS[Users VLAN<br/>(User Devices)]

    IOTC[IOT-Control VLAN<br/>(Control Plane)]
    IOT[IOT VLAN<br/>(Untrusted Devices)]
    GUESTS[Guests VLAN<br/>(Internet Only)]

    FW[pfSense<br/>Firewall / Router]
    WAN[Internet]

    %% VLANs connect only via firewall
    MGMT --> FW
    SERVERS --> FW
    USERS --> FW
    IOTC --> FW
    IOT --> FW
    GUESTS --> FW

    %% Allowed flows
    USERS -->|ALLOW| IOTC
    IOT -->|ALLOW| IOTC

    %% Conditional flows
    IOTC -.->|COND| IOT
    IOTC -.->|COND| SERVERS
    MGMT -.->|COND| SERVERS
    MGMT -.->|COND| IOTC

    %% Internet access
    FW --> WAN
