DHCP Configuration Lab – Cisco Packet Tracer

📌 Overview

This lab demonstrates the configuration and verification of Dynamic Host Configuration Protocol (DHCP) on a Cisco router using Cisco Packet Tracer.

🎯 Objectives

- Configure a Cisco router as a DHCP server
- Create a DHCP address pool
- Configure the default gateway and DNS server
- Exclude reserved IP addresses
- Verify dynamically assigned IP addresses
- Test network connectivity

🛠️ Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI
- DHCP
- IPv4

⚙️ Configuration

Example DHCP configuration:

ip dhcp excluded-address <start-IP> <end-IP>

ip dhcp pool LAN
network <network-address> <subnet-mask>
default-router <gateway-IP>
dns-server <DNS-IP>

🔍 Verification Commands

show ip dhcp binding
show ip dhcp pool
show ip dhcp conflict
show running-config

📚 Key Concepts Practiced

- DHCP Server
- DHCP Address Pool
- IP Address Allocation
- Default Gateway
- DNS Server
- DHCP Excluded Addresses
- DHCP Lease Verification

✅ Result

Successfully configured a Cisco router as a DHCP server and verified dynamic IP address allocation to network devices.

📁 Lab File

The Cisco Packet Tracer ".pkt" file is included in this folder for practice and reference.
