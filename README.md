# Raspberry Pi NAS & Media Server

This repository documents the configuration and operation of my Debian-based NAS and media server deployed on a Raspberry Pi 5.
The system provides centralized storage, authenticated file sharing, and LAN-based media streaming.

---

## Scope

This repository focuses on:
- Storage configuration
- File sharing
- Media delivery
- Host-level security and monitoring

Network architecture, DNS filtering, and routing are documented separately.

---

## Platform

- Hardware: Raspberry Pi 5
- Operating System: Raspberry Pi OS (Debian Bookworm, ARM64)
- Storage: External 2.5" USB HDD

---

## Storage

- Filesystem: EXT4
- Mount point: `/srv/nas`
- Persistent mounting configured via `/etc/fstab`
- Storage organized for media, shared files, and backups

---

## File Sharing

- Service: Samba (SMB)
- Access model: Authenticated users only
- Supported clients: Windows and macOS
- Protocols: SMB2 / SMB3
- Permissions managed through group-based access

Guest access and SMBv1 are disabled.

---

## Media Server

- Service: Jellyfin
- Access: trusted network zone only, remote connections disabled
- Playback mode: Direct Play preferred
- Clients: Web browsers, smart TVs, and mobile devices

Jellyfin is used instead of SMB for media playback on TVs to improve compatibility and usability.

---

## System Management

- Cockpit used for:
  - Service management
  - Resource monitoring
  - Storage visibility

Cockpit is used for administration only, not end-user access.

---

## Disk Health

- SMART monitoring enabled via smartmontools
- Disk health verified via CLI
- Background monitoring configured

SMART data is not exposed in Cockpit due to USB enclosure limitations.

---

## Security

- No host firewall: filtering is done by the network firewall's per-service policies
- Only the services listed above are reachable, and only from the trusted zone
- The server zone cannot start connections to client devices
- No WAN exposure
- No anonymous shares
- Unused services disabled (printing, Bluetooth, modem management, NetBIOS browsing)

---

## Network Placement

The server sits in a dedicated server zone of the segmented homelab network:
- Wired only, Wi-Fi disabled
- Static address in the server zone
- Clients reach shares, Jellyfin and Cockpit by local hostname rather than IP
- Hosts Pi-hole, the network-wide DNS filter for the trusted zone
- Time synced from the network firewall

---

## Related Repository

- **Homelab Network Infrastructure**  
  https://github.com/swimmyOS/homelab-network-documentation/tree/main

---

## Notes

This project emphasizes:
- Correct service configuration
- Practical security controls
- Cross-platform compatibility
- Reproducibility and documentation

---

## Author

Joseph Leahy Jr.  
IT & Cybersecurity  
https://www.linkedin.com/in/joseph-l-904673159  
