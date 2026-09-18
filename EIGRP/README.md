EIGRP Routing Lab – Cisco Packet Tracer

📌 Overview

This lab demonstrates the configuration and verification of Enhanced Interior Gateway Routing Protocol (EIGRP) using Cisco Packet Tracer.

🎯 Objectives

- Configure EIGRP between multiple routers
- Configure router interfaces and IP addressing
- Advertise networks using EIGRP
- Understand EIGRP neighbor relationships
- Verify EIGRP routes and routing information
- Practice basic routing troubleshooting

🛠️ Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI
- EIGRP

⚙️ Configuration

EIGRP was configured using the following commands:

router eigrp 100
network <network-address>
no auto-summary

🔍 Verification Commands

show ip eigrp neighbors
show ip route eigrp
show ip protocols
show ip eigrp topology

📚 Key Concepts Practiced

- EIGRP Neighbor Relationship
- EIGRP AS Number
- Network Advertisement
- Successor and Feasible Successor
- EIGRP Metric
- Routing Table Verification
- Basic Troubleshooting

✅ Result

Successfully configured and verified EIGRP routing between routers in Cisco Packet Tracer.

📁 Lab File

The Cisco Packet Tracer ".pkt" file is included in this folder for practice and reference.
