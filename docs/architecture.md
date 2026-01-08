# Network Architecture

## Segmentation Strategy
The lab utilizes a **Dual-Bridge Architecture** to ensure complete isolation from the home production network.

### Virtual Bridges
1. **vmbr0 (WAN Uplink):** - Linked to physical NIC.
   - Provides internet egress via Linksys Home Router.
   - IP Assignment: DHCP Reservation (`192.168.1.20`).
2. **vmbr1 (Secure Lab LAN):**
   - Air-gapped (No physical NIC).
   - Serves as the backbone for all Lab VMs.

### Gateway Logic
- **Gateway Device:** pfSense VM
- **LAN IP:** `10.0.0.1/24`
- **DHCP Pool:** `10.0.0.10 - 10.0.0.100`
- **Routing:** All `10.0.0.0/24` traffic must traverse pfSense to reach `vmbr0`.
