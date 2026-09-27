# Cisco Packet Tracer – Syslog Configuration Lab

## Overview
This project is a hands-on networking lab built in Cisco Packet Tracer to demonstrate
configuration and troubleshooting of Syslog on a Cisco router (2911 series). The lab
covers console-based logging, VTY line monitoring, buffered logging, and remote
syslog server integration.

## Topology

| Device | Role | IP Address |
|--------|------|------------|
| R1 (Cisco 2911) | Router being configured | 192.168.1.1 |
| SW1 | Layer 2 Switch | 192.168.1.2 |
| PC1 | Client PC (Telnet access) | 192.168.1.10 |
| PC2 | Console cable access | N/A (no IP needed) |
| SRV1 | Syslog Server | 192.168.1.100 |

## Key Concepts Covered
- Local user authentication and enable password configuration
- Enabling/disabling interfaces and observing syslog messages
- Understanding syslog severity levels (0–7)
- Timestamping log messages
- Difference between console logging and VTY (Telnet) logging
- Enabling `terminal monitor` for VTY sessions
- Configuring buffered logging with a custom buffer size
- Sending logs to an external syslog server at a specified severity level

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

! --- Timestamps for logging ---
service timestamps log datetime msec

! --- Interfaces ---
interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
 exit

interface GigabitEthernet0/1
 shutdown
 exit

! --- Buffered logging ---
logging buffered 8192

! --- Syslog server logging ---
logging host 192.168.1.100
logging trap debugging

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
Enable the Syslog service from the **Config → Services → SYSLOG** tab on the server.

---

## Lab Tasks & Testing

### Task 1 – Console Access & Interface Logging
Connect to R1 via console (PC2). Shut down and re-enable the unused interface to observe syslog messages:
```
enable
configure terminal
interface GigabitEthernet0/0
 shutdown
```
Wait for the syslog message, then:
```
no shutdown
```
**Observed severity levels:**
- `%LINK-3-UPDOWN` → Severity 3 (Error)
- `%LINEPROTO-5-UPDOWN` → Severity 5 (Notice)

### Task 2 – Telnet & VTY Logging
From PC1:
```
telnet 192.168.1.1
```
Login: `jeremy` / password: `ccna`

On R1:
```
enable
configure terminal
interface GigabitEthernet0/1
 no shutdown
 exit
```
By default, syslog messages only appear on the console, not on VTY (Telnet) sessions.
To view them during the current Telnet session:
```
terminal monitor
```

### Task 3 – Buffered Logging
```
configure terminal
logging buffered 8192
```
Verify with:
```
show logging
```

### Task 4 – Syslog Server Logging
```
configure terminal
logging host 192.168.1.100
logging trap debugging
```

---

## Verification Commands
```
show running-config
show logging
show ip interface brief
```

## Tools Used
- Cisco Packet Tracer

## Purpose
Built as part of CCNA-level practice to reinforce understanding of network
device logging, syslog severity levels, and remote log management — essential
topics for network monitoring and troubleshooting.
