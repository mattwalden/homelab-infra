flowchart LR
  %% Zones
  MGMT["VLAN 10 MGMT (Management)"]
  SERVERS["VLAN 20 Servers (Trusted Services)"]
  USERS["VLAN 40 USERS (User Devices)"]

  IOTC["VLAN 25 IOT-CONTROL (Control Plane)"]
  IOT["VLAN 30 IOT (Untrusted Devices)"]
  GUESTS["VLAN 50 GUESTS (Internet Only)"]

  FW["pfSense (Firewall/Router)"]
  WAN["Internet"]

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
  IOT
