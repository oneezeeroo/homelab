# Operating the Tailscale Exit Node

## Purpose

Use linux01 as an optional internet gateway for a remote laptop. Files are saved on the remote laptop. Nothing needs to be downloaded onto PVE01.

This runbook describes the setup that worked, how to turn the service on and off, and which security checks still need to be completed.

## Prerequisites

Tailscale must be installed and authenticated on linux01 and the remote laptop. linux01 must have a working connection to the home router and the internet. The tailnet administrator must approve linux01 as an exit node.

## Confirm forwarding on linux01

```bash
sysctl net.ipv4.ip_forward net.ipv6.conf.all.forwarding
```

Both values should be 1. Persistent settings were placed in `/etc/sysctl.d/99-tailscale.conf` during initial setup.

## Advertise the exit node

```bash
sudo tailscale set --advertise-exit-node
```

Approve the exit node under the linux01 machine in the Tailscale admin console if it is not already approved.

To inspect the advertised routes:

```bash
tailscale debug prefs | grep -A 5 AdvertiseRoutes
```

The exit node advertises the IPv4 and IPv6 default routes.

## Start a remote session

1. On the Windows laptop, open Tailscale.
2. Choose linux01 in the Exit Node menu.
3. Open a public IP checking website.
4. Confirm that the reported public IP matches the home internet connection.
5. Use approved applications and save files directly on the laptop.

Avoid relying only on the browser test to verify a specific application's network binding.

## Stop using the exit node

On the Windows laptop, select None in the Tailscale Exit Node menu. Normal internet routing should resume while Tailscale remains available for direct access to the homelab.

This is the preferred routine shutdown because it does not disturb linux01 or Proxmox administration.

If the exit node should be unavailable to other tailnet devices as well, stop advertising it on linux01:

```bash
sudo tailscale set --advertise-exit-node=false
```

The normal Tailscale connection remains in place. Advertise it again when needed.

## Troubleshooting

If public IP verification does not show the home connection, confirm that the laptop selected linux01, check Tailscale status on both devices, and verify that forwarding is enabled. If connectivity degrades, select None as the exit node before changing server configuration.

If an application keeps using a different interface, check its interface binding and test disconnection behavior separately.

## Recovery from firewall experiments

A custom nftables table named `homelab_exit` was used temporarily during testing and removed by an automatic rollback. Do not run the default nftables configuration file without reviewing it because it contains a command that flushes the active ruleset.

The saved experimental rules live under `/etc/nftables.d/`, but they have not been accepted as a permanent security policy. Do not apply them blindly. A prior rollback script was created at `/usr/local/sbin/homelab-firewall-rollback` to delete only the custom table.

## Security and operating notes

The exit node works, but complete home LAN isolation has not been verified. The tailnet policy shown in the session began with broad access. A narrower policy was drafted for review, but a successful save was not established.

Never expose the Proxmox management interface to the public internet for this workflow. Keep Tailscale and Ubuntu updated. Follow the remote network's VPN policies and use downloads only where authorized.
