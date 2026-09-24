. FHRP — First Hop Redundancy Protocol

Provides **default gateway redundancy**. If a router acting as the default gateway fails, another router takes over transparently — hosts keep using the same gateway IP/MAC without reconfiguration.

### Why It's Needed

Hosts are configured with **one** default gateway. If that router goes down, hosts lose connectivity outside their subnet — unless a backup router seamlessly takes over the gateway role.

### The 3 Main FHRPs (Cisco Context)

| Protocol | Type | Vendor | Notes |
|---|---|---|---|
| **HSRP** (Hot Standby Router Protocol) | Cisco proprietary | Cisco | Active/Standby model |
| **VRRP** (Virtual Router Redundancy Protocol) | Open standard (RFC) | Multi-vendor | Master/Backup model |
| **GLBP** (Gateway Load Balancing Protocol) | Cisco proprietary | Cisco | Active/Active — load balancing across routers |

### HSRP Basics

- Routers share a **virtual IP** and **virtual MAC** (`0000.0C07.ACxx`, xx = group number in hex).
- One router is **Active**, one is **Standby**; others are **Listen**.
- Elected by highest **priority** (default 100); tie broken by highest IP.
- Hello timer: 3 sec / Hold timer: 10 sec (default).

```
Router(config)# interface gig0/0
Router(config-if)# ip address 192.168.1.2 255.255.255.0
Router(config-if)# standby 1 ip 192.168.1.1
Router(config-if)# standby 1 priority 110
Router(config-if)# standby 1 preempt
```

- `preempt` — lets a higher-priority router reclaim Active role once it comes back up.
- Verify: `show standby brief`

### VRRP Basics

- Virtual MAC: `0000.5E00.01xx`
- Roles: **Master** / **Backup** (no "Standby" state)
- Default priority 100, range 1–254

```
Router(config-if)# vrrp 1 ip 192.168.1.1
Router(config-if)# vrrp 1 priority 110
```

### GLBP Basics

- One **AVG** (Active Virtual Gateway) assigns different **AVFs** (Active Virtual Forwarders) to load-balance traffic — all routers can forward simultaneously, unlike HSRP/VRRP.

```
Router(config-if)# glbp 1 ip 192.168.1.1
Router(config-if)# glbp 1 priority 110
```

### Quick Comparison

| Feature | HSRP | VRRP | GLBP |
|---|---|---|---|
| Vendor | Cisco | Standard | Cisco |
| Active routers | 1 | 1 | Multiple (load balancing) |
| States | Active/Standby/Listen | Master/Backup | Active/Standby (AVG/AVF) |
