# Cisco Discovery Protocol (CDP)

**Cisco Discovery Protocol (CDP)** is a proprietary Data Link Layer (Layer 2) network protocol developed by Cisco Systems. It allows Cisco devices to discover information about other directly connected Cisco devices on the same network segment.

## Overview
- **Layer:** Data Link Layer (Layer 2)
- **Vendor:** Cisco proprietary (not routable, not IP-dependent)
- **Purpose:** Neighbor discovery and network topology mapping
- **Default behavior:** Enabled by default on most Cisco devices
- **Transmission:** Multicast frames sent periodically (default: every 60 seconds)
- **Holdtime:** Default 180 seconds before a neighbor entry expires

## Information Shared via CDP
- Device ID (hostname)
- IP address
- Platform/hardware model
- Local and remote port identifiers
- Software version (IOS version)
- Device capabilities (router, switch, etc.)
- Native VLAN (on trunk ports)
- Duplex setting

## Common Commands (Cisco IOS)
\`\`\`
show cdp neighbors
show cdp neighbors detail
show cdp interface
show cdp traffic
no cdp run          ! disable CDP globally
no cdp enable        ! disable CDP on an interface
\`\`\`

## Security Considerations
CDP broadcasts sensitive network information in plaintext and can be exploited for reconnaissance. Best practice is to disable it on interfaces facing untrusted networks or the public internet.

## Related Protocols
- **LLDP** (Link Layer Discovery Protocol) — vendor-neutral equivalent, defined in IEEE 802.1AB
