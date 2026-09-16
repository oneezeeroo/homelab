# Incident: Pi-hole Installer Hung on dns01

## Summary

During the initial Pi-hole installation on `dns01`, the installer repeatedly stalled at the dependency-installation stage. The original console session eventually became unresponsive, and SSH access also required recovery.

## Symptoms

- Pi-hole installer remained at the dependency package step for an extended period
- `Ctrl+C` did not reliably restore the original console
- A stale console session remained visible in Proxmox
- SSH service was not immediately reachable after recovery attempts

## Investigation

A second session was used to check for active package-management processes:

```bash
ps aux | grep -E 'apt|dpkg|pihole'
```

Package-manager consistency was checked with:

```bash
sudo dpkg --configure -a
sudo apt -f install
```

SSH socket activation was restored with:

```bash
sudo systemctl enable --now ssh.socket
```

## Resolution

The Pi-hole installer ultimately proceeded when executed from a true root shell:

```bash
sudo -i
curl -sSL https://install.pi-hole.net | bash
```

After installation:

- Pi-hole DNS filtering was verified
- The VM received a DHCP reservation
- Pi-hole survived a VM reboot/reset
- DNS blocking was confirmed from another VM
- A known-good Proxmox snapshot was created

## Validation

A normal DNS query resolved successfully while a known advertising/tracking domain returned the Pi-hole blocking response.

## Lessons learned

1. Do not assume a frozen terminal means a process is still running.
2. Use a second session to inspect `apt`, `dpkg`, and service state.
3. Restore package-manager health before repeatedly rerunning installers.
4. Test services after reboot before taking a baseline snapshot.
5. Record troubleshooting while the details are still fresh.
