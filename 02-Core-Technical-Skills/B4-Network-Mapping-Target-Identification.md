# Network Mapping & Target Identification

## Analysis of output from tools used to map the route between the engagement point and a number of targets.

To map the route between the testing machine and the targets, you could use PathPing or Traceroute, assuming ICMP echo-reply is not blocked on the firewalls. If the firewalls are blocking ICMP protocol, you could attack to map the path using Traceroute with UDP packets. Again this assumes UDP 33434 - 33534 is not blocked.

**Traceroute Example:**

```bash
traceroute to nepal.gov.np (202.45.147.252), 64 hops max, 52 byte packets

 1  10.28.0.1 (10.28.0.1)  478.335 ms  76.807 ms  73.279 ms

 2  vlan156.as06.mia1.us.m247.com (45.87.214.193)  163.392 ms  114.015 ms  296.273 ms

 3  217.138.223.222 (217.138.223.222)  100.249 ms

    217.138.223.210 (217.138.223.210)  73.814 ms  87.646 ms

 4  te0-3-1-14.201.nr51.b002802-5.mia01.atlas.cogentco.com (38.140.53.65)  123.359 ms

    te0-2-1-9.nr51.b002802-5.mia01.atlas.cogentco.com (38.104.90.217)  325.528 ms  87.053 ms

 5  be3763.rcr21.b002802-2.mia01.atlas.cogentco.com (154.24.30.129)  80.090 ms  84.957 ms  74.048 ms

 6  be3410.ccr21.mia01.atlas.cogentco.com (154.54.6.85)  77.727 ms  76.056 ms

    be3411.ccr22.mia01.atlas.cogentco.com (154.54.26.41)  107.551 ms

 7  be3570.ccr42.iah01.atlas.cogentco.com (154.54.84.1)  106.891 ms

    be3569.ccr41.iah01.atlas.cogentco.com (154.54.82.241)  110.317 ms

    be3570.ccr42.iah01.atlas.cogentco.com (154.54.84.1)  105.195 ms

 8  be2927.ccr21.elp01.atlas.cogentco.com (154.54.29.222)  129.740 ms

    be2928.ccr21.elp01.atlas.cogentco.com (154.54.30.162)  120.706 ms  139.252 ms

 9  be2930.ccr32.phx01.atlas.cogentco.com (154.54.42.77)  126.139 ms  134.253 ms  125.011 ms

10  be2931.ccr41.lax01.atlas.cogentco.com (154.54.44.86)  141.096 ms  137.965 ms

    be2932.ccr42.lax01.atlas.cogentco.com (154.54.45.162)  137.944 ms

11  be3360.ccr41.lax04.atlas.cogentco.com (154.54.25.150)  142.443 ms  137.632 ms

    be3271.ccr41.lax04.atlas.cogentco.com (154.54.42.102)  139.926 ms

12  38.122.147.122 (38.122.147.122)  139.789 ms  203.835 ms  306.701 ms

13  116.119.68.100 (116.119.68.100)  409.570 ms

    182.79.134.219 (182.79.134.219)  409.480 ms

    116.119.68.100 (116.119.68.100)  525.812 ms

14  125.17.159.10 (125.17.159.10)  407.898 ms  410.622 ms  1126.678 ms

15  but.core-bhr.core.ntc.net.np (202.70.93.73)  920.725 ms  571.759 ms  715.819 ms

16  ptn.core-but.core.ntc.net.np (202.70.93.110)  511.481 ms  612.101 ms  386.669 ms

17  ptn.acc-ptn.core.ntc.net.np (202.70.93.95)  409.220 ms  405.307 ms  472.254 ms

18  ptn.acc-ptn.ne.acc.ntc.net.np (202.70.93.100)  511.400 ms  990.081 ms  771.333 ms

19  202.70.79.1 (202.70.79.1)  541.801 ms  378.448 ms  396.731 ms

20  sumo-147-242.nitc.gov.np (202.45.147.242)  417.438 ms  392.895 ms  370.286 ms

21  144-162.nitc.gov.np (202.45.145.162)  449.133 ms  408.488 ms  409.836 ms

22  sumo-147-252.nitc.gov.np (202.45.147.252)  380.957 ms  374.867 ms  395.175 ms

23  sumo-147-252.nitc.gov.np (202.45.147.252)  378.706 ms  407.475 ms  495.505 ms

24  sumo-147-252.nitc.gov.np (202.45.147.252)  425.910 ms  407.672 ms  424.088 ms
```

**Understanding the output:**

- The first hop 10.28.0.1 is the local gateway
- Hop 2 `vlan156.as06.mia1.us.m247.com` hits the service provider network of `m247`.
- Hop 3 shows 2 IP addresses, possibly due to load balancing
- Hop 4 moves into the `ISP` network of `cogentco.com` or Cogent Communications.
- Checking the IPs on hop 12 and 13, you can see the route moving out of the US to India. We can determine whis by checking the IP assignments of Whois or other IP allocation viewers.
*Whois*
```
NetRange:       116.0.0.0 - 116.255.255.255
CIDR:           116.0.0.0/8
NetName:        APNIC-116
NetHandle:      NET-116-0-0-0-1
Parent:          ()
NetType:        Allocated to APNIC
OriginAS:
Organization:   Asia Pacific Network Information Centre (APNIC)
RegDate:        2007-01-17
Updated:        2010-07-30
Comment:        This IP address range is not registered in the ARIN database.
```
- This brings the traceroute request into Asia and by hop 15, the packet is in the Nepal assigned IP allocation.

## Network sweeping techniques to prioritise a target list and the potential for false negatives.

Ping sweeps are often used to determine if a given host is alive. It can be useful to condense a large IP range down by selecting only the hosts confirmed to be active, for further targeted port scanning. The idea is to same time by not port scanning a host that is down.

Ping sweeps can be done in a few ways:

| Technique| Pros| Cons|
|----------|-----|-----|
ICMP Ping| Quick results and likely to be accurate if a response is sent back| ICMP Pings are typically blocked, so there is the possibility a host marked as down, is not actually down.|
|TCP/UDP Ping|More likely to not be blocked by firewalls.| Relies on a well known service/port being open, so could still present false negatives.