Standard Access Lists

Filter traffic only by source IP address. Numbered range: 1–99 (and 1300–1999 for expanded).

Router(config)# access-list 10 permit 192.168.1.0 0.0.0.255
Router(config)# access-list 10 deny any

Router(config)# interface gig0/0
Router(config-if)# ip access-group 10 out
Should be placed close to the destination (since they can't filter by destination/port, placing them near the source would block too much).
Wildcard mask 0.0.0.255 = match first 3 octets, ignore last.

Named version:

Router(config)# ip access-list standard BLOCK_SUBNET
Router(config-std-nacl)# permit 192.168.1.0 0.0.0.255
Router(config-std-nacl)# deny any
Extended Access Lists

Filter by source IP, destination IP, protocol, and port. Numbered range: 100–199 (and 2000–2699 expanded).

Router(config)# access-list 110 permit tcp 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255 eq 80
Router(config)# access-list 110 deny ip any any

Router(config)# interface gig0/1
Router(config-if)# ip access-group 110 in
Should be placed close to the source (to stop unwanted traffic early, since they're specific enough not to overblock).

Named version:

Router(config)# ip access-list extended ALLOW_WEB
Router(config-ext-nacl)# permit tcp any host 192.168.2.10 eq 443
Router(config-ext-nacl)# deny ip any any
Key differences
	Standard	                            Extended
Filters on   	Source IP only	           Source/Dest IP, protocol, port
Number range	1–99, 1300–1999            100–199, 2000–2699
Placement    	Near destination           Near source
Precision    	Coarse	                   Fine-grained
Verification
show access-lists
show ip interface gig0/0
