# Virtual Machine Inventory

## linux01

**Platform:** Ubuntu Server  
**Purpose:** Linux administration, SSH, networking tools, testing, and future automation  
**Resources:** 2 vCPU, 2 GB RAM, 32 GB virtual disk  
**Remote access:** SSH and Tailscale  
**DNS:** Uses dns01 / Pi-hole

## dns01

**Platform:** Ubuntu Server  
**Purpose:** Pi-hole DNS filtering  
**Resources:** 1 vCPU, 1 GB RAM, 16 GB virtual disk  
**Addressing:** DHCP reservation on the home gateway  
**Status:** Filtering verified and reboot tested

### Baseline snapshot
`baseline-pihole-working`

## Planned VMs

- **fw-lab01** — isolated OPNsense firewall/router learning environment
- **app01** — Docker/Portainer application host
- **mon01** — monitoring/NOC services
- **dc01** — Windows Server / Active Directory
- **siem01** — Wazuh SIEM
- **jump01** — future privileged management jump host
