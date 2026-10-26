# Architecture

## Design principle

The lab is being built as a miniature enterprise rather than a collection of unrelated self-hosted applications.

The core rule is:

> If one component is compromised, what can it reach next?

This drives segmentation, firewall rules, container networks, identity boundaries, and service permissions.

## Current physical topology

```text
Internet
   |
ISP Gateway
   |
SW01
   |
   +-- PC01
   +-- PVE01
   +-- ADMIN01 / future PVE03
```

## Current virtual topology

```text
PVE01
├── linux01
└── dns01
    └── Pi-hole
```

## Planned compute layout

```text
                 SW01
                   |
       +-----------+-----------+
       |           |           |
     PVE01       PVE02       PVE03
   Primary VM    Apps /      Utility /
      host       Docker       quorum
```

## Planned security layers

```text
Physical VLAN
    ↓
Firewall policy
    ↓
VM / host boundary
    ↓
Container network
    ↓
Application authentication
```

## Planned service zones

- Management
- Users
- Servers
- Lab
- IoT
- Guest
- DMZ
- Security
- Isolated testing

The physical VLAN rollout will happen only after the design has been tested virtually.

## Remote internet gateway

linux01 now advertises an approved Tailscale exit node. A remote laptop can choose it for internet routing and continue storing downloads locally. The VM forwards traffic to the home router; it is not a download server or storage share.

```text
Remote laptop
      |
Tailscale tunnel
      |
linux01 on PVE01
      |
Home gateway
      |
Internet
```

The laptop can deselect the exit node for normal routing without losing direct Tailscale access to the lab. This design avoids adding another workload or storage requirement to the OptiPlex.

The connection and management access have been verified. An experimental firewall table was removed after a successful rollback test. Complete home LAN isolation and final tailnet access restrictions still require verification. See [the project notes](remote-exit-node.md).
