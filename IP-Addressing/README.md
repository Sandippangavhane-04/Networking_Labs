IP Addressing Lab – Cisco Packet Tracer

📌 Overview

This lab demonstrates the configuration and verification of IPv4 addresses on Cisco routers and network devices using Cisco Packet Tracer.

🎯 Objectives

- Understand IPv4 addressing
- Configure IP addresses on router interfaces
- Configure subnet masks
- Configure default gateways where required
- Verify interface IP configuration
- Test network connectivity

🛠️ Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI
- IPv4 Addressing

⚙️ Configuration

Example Cisco IOS configuration:

interface gigabitEthernet 0/0
ip address <IP-address> <subnet-mask>
no shutdown

🔍 Verification Commands

show ip interface brief
show ip interface
show running-config
ping <destination-IP>

📚 Key Concepts Practiced

- IPv4 Addressing
- Subnet Mask
- Network Address
- Host Address
- Default Gateway
- Interface Configuration
- Connectivity Testing

✅ Result

Successfully configured and verified IPv4 addressing on Cisco network devices and tested connectivity using ping.

📁 Lab File

The Cisco Packet Tracer ".pkt" file is included in this folder for practice and reference.
