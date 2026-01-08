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

## Network Segmentation Logic
The environment uses a **Segmented Gateway** model.

* **WAN Bridge (vmbr0):** Connects to the physical Linksys network. 
* **LAN Bridge (vmbr1):** Isolated virtual switch with no physical NIC.
* **Firewall (pfSense):** - WAN IP: 192.168.1.20 (Static via Linksys DHCP Reservation)
    - LAN IP: 10.0.0.1/24 (Lab Default Gateway)
    - **Note:** RFC1918 blocking disabled on WAN to allow management via 192.168.1.0/24.
