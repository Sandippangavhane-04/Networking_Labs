# Cisco Packet Tracer – SNMP Configuration Lab

## Overview
This project is a hands-on networking lab built in Cisco Packet Tracer to demonstrate
configuration of SNMP (Simple Network Management Protocol) on a Cisco router (2911 series).
The lab covers SNMP community strings, access control, trap notifications, and
monitoring via an NMS (Network Management Station) / SNMP server.

## Topology

| Device | Role | IP Address |
|--------|------|------------|
| R1 (Cisco 2911) | Router being configured | 192.168.1.1 |
| SW1 | Layer 2 Switch | 192.168.1.2 |
| PC1 | Client PC (Telnet access) | 192.168.1.10 |
| PC2 | Console cable access | N/A (no IP needed) |
| SRV1 | SNMP Server / NMS | 192.168.1.100 |

## Key Concepts Covered
- SNMP versions (v1, v2c, v3) and their differences
- Read-only (RO) and Read-write (RW) community strings
- Restricting SNMP access using ACLs
- Configuring SNMP trap notifications
- Setting the SNMP trap destination (NMS/server)
- Identifying the device using `snmp-server contact` and `snmp-server location`
- Verifying SNMP configuration and traffic

---

## Full Configuration

### SW1 (Switch)
```
enable
configure terminal
hostname SW1

interface vlan 1
 ip address 192.168.1.2 255.255.255.0
 no shutdown
 exit

interface FastEthernet0/1
 switchport mode access
 no shutdown
 exit

interface FastEthernet0/2
 switchport mode access
 no shutdown
 exit

interface GigabitEthernet0/1
 no shutdown
 exit

end
write memory
```

### R1 (Router)
```
enable
configure terminal
hostname R1

! --- Username & Passwords ---
username jeremy password ccna
enable password ccna

! --- Console line ---
line console 0
 login local
 logging synchronous
 exit

! --- VTY lines (Telnet) ---
line vty 0 4
 login local
 logging synchronous
 exit

! --- Interfaces ---
interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
 exit

interface GigabitEthernet0/1
 shutdown
 exit

! --- Access list to restrict SNMP access (only from SRV1) ---
access-list 10 permit host 192.168.1.100

! --- SNMP Community Strings ---
snmp-server community CCNA_RO RO 10
snmp-server community CCNA_RW RW 10

! --- SNMP System Info ---
snmp-server contact jeremy@company.com
snmp-server location Datacenter-Rack1

! --- Enable SNMP Traps ---
snmp-server enable traps
snmp-server host 192.168.1.100 version 2c CCNA_RO

end
write memory
```

### PC1 IP Configuration
```
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
```

### SRV1 IP Configuration
```
IP Address: 192.168.1.100
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
```
Enable SNMP receiving from the **Config → Services → SNMP** tab (if available in your
Packet Tracer version) so the server can act as the NMS and receive trap messages from R1.

---

## Lab Tasks & Testing

### Task 1 – Basic SNMP Setup
Configure read-only and read-write community strings, restricted by ACL:
```
access-list 10 permit host 192.168.1.100
snmp-server community CCNA_RO RO 10
snmp-server community CCNA_RW RW 10
```

### Task 2 – Identify the Device
```
snmp-server contact jeremy@company.com
snmp-server location Datacenter-Rack1
```
Verify with:
```
show snmp
```

### Task 3 – Trigger and Observe an SNMP Trap
Enable traps and point them to the SNMP server:
```
snmp-server enable traps
snmp-server host 192.168.1.100 version 2c CCNA_RO
```
Cause a trap-worthy event (e.g., shut/no shut an interface) and confirm the trap
is received on SRV1:
```
interface GigabitEthernet0/1
 shutdown
 no shutdown
```

### Task 4 – Verify SNMP Communication
From the SNMP server (SRV1), poll R1 using the RO community string and confirm
values such as system uptime, interface status, and hostname can be retrieved.

---

## Verification Commands
```
show running-config
show snmp
show snmp community
show access-lists
```

## Tools Used
- Cisco Packet Tracer

## Purpose
Built as part of CCNA-level practice to reinforce understanding of SNMP
community strings, access restriction, trap notifications, and remote
device monitoring — essential topics for network management.
