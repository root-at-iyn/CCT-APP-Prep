# Filtering Avoidance Techniques

## The importance of egress and ingress filtering, including the risks associated with outbound connections.

### Ingress Filtering 
Ingress filtering is a network security best practice to control network traffic coming into a network. When you implement ingress filters, you are blocking network traffic from either:
- source IP / networks
- TCP/UDP ports (traffic directed to a tcp port, or coming from a source port)
- Protocol types (ICMP, SMB, SNMP ... etc.)
- Traffic patterns (malicious traffic patterns with known signatures, usually picked up by IPS devices)

Ref: https://www.ncsc.gov.ie/emailsfrom/Resources/Ingress-Egress/

> Ingress filtering is a simple and effective method to limit the impact of a Denial of Service (DoS) attack, by denying traffic with a forged IP source address (IP spoofing) access to the network, and help ensure that traffic is traceable to its correct network.

It can help prevent servers in the network from communicating with services not sanctioned by IT Policy, e.g. rougue software registries, services known to be used to transport malware, administrative network services (DNS, SNMP, SSH. SMB) directed to servers outside of the organisations administrative control.

### Egress Filtering

Egress filtering is performed to control the traffic that leaves the network.  
> Egress filtering is primarily achieved through the use of predefined security rules and policies implemented on the perimeter firewall, to block outbound traffic that uses protocols and destination ports that are unnecessary or subject to abuse. 

## Avoiding Filtering (Hackers perspective)
Avoiding filtering on Netowork and Host-Based Firewalls can be done via:
- **TTL Manipulation**: Simplying modifing the TTL Value in the packet.
- **Avoiding IPS/IDS signatures**: Adding arbitrary data to the packet or increasing the data length to a large number
- **Packet Fragmentation**: Some IPS devices will not handle fragmentation
- **Invalid checksums**: Sensors usually don't calculate checksum for performance reasons
- **Uncommon IP and TCP options**: Some sensors may discard / ignore packets with certain IP Options, but the destination host may accept them.

Ref:
- https://github.com/vecna/sniffjoke (Tool used to scramble packets)
- https://book.hacktricks.xyz/generic-methodologies-and-resources/pentesting-network/ids-evasion
- https://scapy.net/ (Packet manipulater)
