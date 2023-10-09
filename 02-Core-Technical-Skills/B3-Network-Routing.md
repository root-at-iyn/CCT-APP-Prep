# Network Routing

## RIP
Routing Information Protocol (RIP) is a distance-vector routing protocol. Routers running the distance-vector protocol send all or a portion of their routing tables in routing-update messages to their neighbors. 

RIP prevents routing loops by implementing a limit on the number of hops allowed in a path from source to destination. The largest number of hops allowed for RIP is 15, which limits the size of networks that RIP can support. Ref (https://en.wikipedia.org/wiki/Routing_Information_Protocol)

- ### RIP
    - Uses classful routing
    - No router authentication
    - Attacks:
        - Succceptible to spooofed updates
        - 
- ### RIPv2
    - Supports Classless Inter-Domain Routing (CIDR)
    - Multicasts the route-table to adjacent neighor routers
    - Suopprts route tags to determine routes learned from RIP vs other protocols
    - Supports MD5 authentication
    - Attacks:
        - Capture and crack MD5 hash
- ### RIPng
    - Extends RIPv2
    - Does not support RIPv1 updates authentication
    - Supports IPv6
    - Encodes the next-hop into each each route entry
    - Sends updates on `UDP 521` using multicast `ff02::9`
## OSPF
Open Shortest Path First (OSPF) is a routing protocol for Internet Protocol (IP) networks. It uses a link state routing (LSR) algorithm and falls into the group of interior gateway protocols (IGPs), operating within a single autonomous system (AS).

OSPF gathers link state information from available routers and constructs a topology map of the network. The topology is presented as a routing table to the internet layer for routing packets by their destination IP address. OSPF supports Internet Protocol version 4 (IPv4) and Internet Protocol version 6 (IPv6) networks and is widely used in large enterprise networks.
- Uses HELO packets to Multicast 224.0.0.5
- Every router in the topology knows the status of the OSPF area
- Does not enforce authentication, but supports MD5
- Attacks:
    - Capture and crack MD5 hash
## IGRP
Interior Gateway Routing Protocol (IGRP) is a distance vector interior gateway protocol (IGP) developed by Cisco. It is used by routers to exchange routing data within an autonomous system.

IGRP is a proprietary protocol. IGRP was created in part to overcome the limitations of RIP (maximum hop count of only 15, and a single routing metric) when used within large networks.
- Supports route metrics (bandwidth, delay, load, reliability)
- Classful routing
- No authentication
- Attacks:
    - Succceptible to spooofed updates
    - Denial of Service
    - Routing loops
## EIGRP
Enhanced Interior Gateway Routing Protocol (EIGRP) is an advanced distance-vector routing protocol that is used on a computer network for automating routing decisions and configuration. The protocol was designed by Cisco Systems as a proprietary protocol, available only on Cisco routers.

EIGRP is used on a router to share routes with other routers within the same autonomous system. Unlike other well known routing protocols, such as RIP, EIGRP only sends incremental updates, reducing the workload on the router and the amount of data that needs to be transmitted.
- Supports MD5 and SHA-2 authentication between neighboring routers.
- Sends topology changes 
- Backward compatible with IGRP
- Attacks:
    - Capture of EIGRP broadcasts, and manipulation route configuration
