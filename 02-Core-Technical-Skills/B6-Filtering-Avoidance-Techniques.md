# Filtering Avoidance Techniques

## The importance of egress and ingress filtering, including the risks associated with outbound connections.

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
