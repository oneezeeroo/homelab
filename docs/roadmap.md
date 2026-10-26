# Roadmap

## Phase 1 — Physical foundation

- [x] Run wired Ethernet from ISP gateway to lab location
- [x] Install managed switch
- [x] Verify Gigabit connectivity
- [x] Document switch port roles

## Phase 2 — Primary virtualization

- [x] Install Proxmox VE on PVE01
- [x] Configure secure remote access with Tailscale
- [x] Build linux01
- [x] Build dns01
- [x] Install and verify Pi-hole
- [ ] Build fw-lab01 with OPNsense

## Phase 3 — Virtual networking lab

- [ ] Create isolated virtual networks
- [ ] Learn DHCP and DNS across routed segments
- [ ] Practice NAT
- [ ] Practice stateful firewall rules
- [ ] Introduce lab VLANs virtually
- [ ] Capture and analyze traffic

## Phase 4 — Application platform

- [ ] Add PVE02 mini PC
- [ ] Build app01
- [ ] Install Docker
- [ ] Install Portainer
- [ ] Deploy Uptime Kuma
- [ ] Deploy Nginx Proxy Manager
- [ ] Add internal HTTPS
- [ ] Deploy Vaultwarden after backup/recovery controls exist

## Phase 5 — Enterprise services

- [ ] Windows Server / Active Directory
- [ ] Internal DNS design
- [ ] Group Policy
- [ ] PKI / certificates
- [ ] Centralized authentication / SSO

## Phase 6 — Physical segmentation

- [ ] Management VLAN
- [ ] User VLAN
- [ ] Server VLAN
- [ ] Lab VLAN
- [ ] IoT VLAN
- [ ] Guest VLAN
- [ ] DMZ
- [ ] Security VLAN
- [ ] Isolated security-testing VLAN

## Phase 7 — Security operations

- [ ] Centralized logging
- [ ] Wazuh SIEM
- [ ] Suricata
- [ ] Zeek
- [ ] Vulnerability scanning
- [ ] Switch port mirroring / SPAN
- [ ] Incident-response runbooks

## Phase 8 — Automation

- [ ] Git-based configuration
- [ ] Ansible
- [ ] Infrastructure as Code
- [ ] Automated backups
- [ ] Configuration validation

## Phase 9 — Storage

- [ ] Build NAS01
- [ ] Learn ZFS
- [ ] SMB / NFS
- [ ] Backup strategy
- [ ] Storage VLAN
- [ ] 2.5/10 GbE when justified

## Phase 10 — Local AI operations

- [ ] Build dedicated AI01
- [ ] Ingest sanitized security telemetry
- [ ] Summarize alerts and incidents
- [ ] Correlate DNS, firewall, Zeek, Suricata, and Wazuh data
- [ ] Keep remediation human-approved initially

## Remote exit node milestone

I added a working Tailscale exit node to linux01 so my school laptop can use my home internet connection without requiring download storage on the Proxmox host.

**Completed:** Enabled persistent IPv4 and IPv6 forwarding, verified Tailscale managed NAT, approved the exit node, confirmed home internet egress, preserved SSH and Proxmox management access during testing, and demonstrated an automatic rollback of experimental firewall rules.

**Remaining:** Verify least privilege tailnet grants, complete and test isolation from the home LAN, check application binding during VPN disconnection, and document any future network changes that affect the IPv6 prefix.

This work supports Phase 2 remote access, introduces practical Phase 3 routing and firewall skills, and provides material for Phase 8 automation without changing the planned deployment order.
