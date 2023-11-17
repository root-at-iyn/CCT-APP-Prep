# Packet Crafting

## Packet crafting to meet a particular requirement:

All of the IPv4 packet crafting tasks can be perfromed with Nmap's `Nping` utility. The base code of the utility was repurposed from `Hping3`, but is now maintained by Nmap (Fydoor). 

### Modifying source ports

*Send a tcp packet 4 times (`-c`) with a source port of `80`*
```pwsh
nping --tcp -c 4 --source-port 80 10.10.1.10
```

### Spoofing IP addresses

*Send an icmp packet of type `(8) Echo Request` with a source IP of `10.10.1.1`. This simulates spoofing another IP on the same subnet*
```pwsh
nping --icmp --icmp-type echo -c 4  --source-ip 10.10.1.1 10.10.1.10
```
### Manipulating TTL’s

*Sends an echo-request icmp packet with a TTL of 128*
```pwsh
nping --icmp --icmp-type 8 --ttl 128 10.10.1.10
```
### Fragmentation
*Sends a packet with ICMP code (1) `Fragment Reassembly Time Exceeded`*
```pwsh
nping --icmp --icmp-code 1 --ttl 128 10.10.1.10
```

### Generating ICMP packets

*Demonstrated above*

Ref: See Nping man page - https://man7.org/linux/man-pages/man1/nping.1.html