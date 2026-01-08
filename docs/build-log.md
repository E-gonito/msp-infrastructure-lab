# Phase 1 Build Log

## [2025-01-08] - Network Initialization
- Created `vmbr1` on Proxmox host.
- **Issue:** `vmbr1` not active in VM hardware.
- **Resolution:** Installed `ifupdown2` and applied staged changes in PVE GUI.

## [2025-01-08] - pfSense Provisioning
- **Optimization:** Disabled "Hardware Checksum Offloading" to fix VirtIO packet loss.
- **Fix:** Resolved a Subnet Conflict where WAN and LAN both defaulted to `192.168.1.x`. Migrated LAN to `10.0.0.0/24`.
- **Remote Access:** Moved Tailscale from an LXC container directly to the pfSense package to centralize the network edge.
