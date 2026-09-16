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
