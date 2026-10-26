# Remote Internet Access Through Tailscale

## Why I built this

I wanted to use my home internet connection while working remotely without copying large downloads onto the Proxmox server first. I already had Tailscale running on my school laptop and on linux01, so turning linux01 into an exit node was a practical way to learn real network routing while solving a problem I actually had.

The laptop runs the applications and saves the files locally. linux01 only forwards traffic through my home router. This means PVE01 does not need a separate download disk or another VM for this workflow.

## Where it fits in the lab

This project extends the remote administration work in Phase 2 and gives me hands on practice with the routing, NAT, and firewall concepts in Phase 3. It also supports the broader goal of building useful services before buying more hardware.

## How the traffic moves

```text
School laptop
    |
    | Encrypted Tailscale tunnel over the available network
    v
linux01 on PVE01
    |
    | IP forwarding and Tailscale NAT
    v
Home router
    |
    v
Home internet connection
    |
    v
Internet services

Downloaded data returns through the tunnel and is saved on the school laptop.
```

An exit node is not a remote storage server. It changes the route used for internet traffic. The laptop remains responsible for application execution and file storage.

## What I configured

I confirmed that linux01 and my school laptop were connected to the same tailnet. I enabled IPv4 and IPv6 forwarding using a persistent sysctl configuration, checked the existing Tailscale forwarding and NAT rules, advertised both default routes through Tailscale, and approved linux01 as an exit node in the admin console.

I then selected linux01 as the exit node on the Windows laptop. A public IP check showed the expected home internet address. This was the key functional test: the browser was accessing the internet through the home connection rather than exiting directly through the remote network.

I also confirmed that SSH access to linux01 and the Proxmox dashboard remained available during the firewall experiments. This gave me practical experience testing management access separately from forwarding.

## Firewall experiments and actual security status

I examined the iptables rules and the underlying nftables ruleset. Tailscale manages its own firewall chains through the iptables compatibility layer. I created a separate nftables table to experiment with blocking forwarding to the known home IPv4 and IPv6 LAN prefixes, and tested its syntax before loading it.

I used systemd to schedule a temporary rollback, confirmed that the new table was removed when the rollback ran, and checked that Tailscale's forwarding chain remained present. These were useful deployment and recovery tests.

The custom nftables table was not left running. The tested rules only covered known prefixes and did not establish complete network isolation. A more restrictive Tailscale access policy was drafted and previewed, but it was not confirmed as saved. I should not describe this project as having a completed least privilege firewall.

The exit node is functional, but security hardening remains unfinished. Until isolation is tested, devices authorized to use the exit node may be able to reach other destinations on the home network. Direct connections to linux01 are governed separately from forwarded traffic.

## Practical limitations

The exit node forwards general internet traffic, not just one application. Transfer speed may be limited by the home internet upload bandwidth, tunnel path, and remote connection. The remote network still carries encrypted VPN traffic, so its acceptable use requirements still apply.

A public IP check confirms browser egress but does not independently prove that a torrent client's network interface is bound correctly. That binding and a disconnect test remain separate verification tasks. Only download material I am authorized to obtain.

## What comes next

1. Finish a tested least privilege Tailscale policy while preserving management access.
2. Implement firewall rules that handle the real home LAN boundaries and possible IPv6 prefix changes.
3. Verify allowed internet forwarding and denied internal forwarding with actual traffic tests.
4. Confirm application interface binding and the behavior when the VPN disconnects.
5. Add repeatable configuration management and monitoring when the automation phase begins.

This build taught me that a working connection and a secure connection are not the same thing. I learned how to verify each layer instead of assuming that a VPN alone would handle every security decision.
