# HomeLab

A hands-on mini-enterprise homelab built to learn networking, systems administration, cybersecurity, virtualization, automation, and eventually local AI-assisted network operations.

## Current goals

- Build a small enterprise-style network from commodity hardware
- Learn Proxmox virtualization and clustering
- Practice routing, switching, VLANs, DNS, DHCP, firewalls, and VPNs
- Build secure self-hosted services with least-privilege network design
- Add monitoring, centralized logging, SIEM, and network security monitoring
- Automate infrastructure with Git, Ansible, and Infrastructure as Code
- Eventually add a local AI server to assist with log analysis and incident triage

## Current environment

- **PVE01** — Dell OptiPlex 9020, primary Proxmox VE host
- **SW01** — TP-Link TL-SG608E managed Gigabit switch
- **linux01** — Ubuntu Server learning/utility VM
- **dns01** — Pi-hole DNS filtering VM
- **MOB01** — mobile school/admin endpoint used for remote access
- **ADMIN01 / future PVE03** — Dell Latitude E6230, planned lightweight third Proxmox node
- **PVE02** — planned mini PC for application/container workloads

## Remote management

Remote administration currently uses Tailscale. Public Internet exposure of hypervisor management interfaces is intentionally avoided.

## Repository layout

- `docs/` — architecture, networking, security, and roadmap
- `inventory/` — hardware, VMs, and services
- `runbooks/` — repeatable installation and recovery procedures
- `incidents/` — troubleshooting writeups and lessons learned
- `configs/` — sanitized configuration examples only

> This repository is public. Do not commit passwords, API keys, private keys, recovery codes, Tailscale auth keys, tokens, or other secrets.
