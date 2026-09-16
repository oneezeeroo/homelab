# Hardware Inventory

## PVE01 — Primary Virtualization Host

**Model:** Dell OptiPlex 9020  
**CPU:** Intel Core i7-4790  
**RAM:** 16 GB  
**Storage:** 512 GB SSD  
**Role:** Primary Proxmox VE host for infrastructure and lab VMs

### Planned upgrades
- 1 TB SSD
- 2 TB HDD
- Possible multi-port Intel NIC
- RAM expansion if practical

## SW01 — Main Lab Switch

**Model:** TP-Link TL-SG608E  
**Ports:** 8 × 1 GbE  
**Role:** Managed Layer-2 switch for the lab

### Learning use
- 802.1Q VLANs
- Tagged/untagged ports
- Link aggregation
- Port mirroring
- Loop prevention

## ADMIN01 / Planned PVE03

**Model:** Dell Latitude E6230  
**Storage:** 256 GB SSD  
**Role today:** Admin/network workstation  
**Planned role:** Lightweight third Proxmox node / quorum participant / utility workloads

## PC01

Gaming desktop used as a trusted client on the home network.

## MOB01

Primary school/gaming laptop.

**Role:** Mobile endpoint and remote administration workstation via Tailscale.

## Planned PVE02

A used business mini PC is planned as a second Proxmox host, focused on application and container workloads.

### Target specification
- Intel 8th-gen i5 or newer
- 16 GB RAM minimum; 32 GB preferred
- 256 GB SSD minimum; 512 GB+ preferred
- Wired Gigabit Ethernet minimum
- Intel VT-x and VT-d support
