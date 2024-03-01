# OS Fingerprinting

## Remote operating system fingerprinting; active and passive techniques.

Stack fingerprinting is a process that uses techniques to determine a target operating system. This can be done passively or actively, but both methods do not always provide 100% accuracy. Therefore, stack fingerprinting is said to determine the likelihood of the target having a particular operating system (OS).

### Active OS Fingerprinting

When using Active Stack Fingerprinting, it requires you send ICMP, TCP, or UDP traffic to the server. This requires that at least one port is open. There are a number of probes that can be sent to help determine the OS:

|Probe|Description|
|-----|-----------|
|Fin probe||
|Bogus flag probe||
|Initial Sequence Number (ISN) Sampling||
|Do not fragment (DF) bit monitoring||
|TCP Initial Window Size||
|ACK value||
|ICMP error message quenching||
|ICMP error message quoting||
|ICMP error message - echo integrity||
|Type of Service (ToS)||
|Fragmentation handling||
|TCP options||

### Passive OS Fingerprinting

Passive Stack Fingerprinting is another technique that can be used to identify operating systems on the network, however it does not require you to actively send packets to the target systems. Passive fingerprinting is done by capturing packets on the network using a sniffer (usually from a mirrored network port), and analysing the following:
- Time-to-live (TTL): The TTL sent sent from the server.
- Window Size: The Window Size sent by the server (e.g. 0x2798).
- Do Not Fragment (DF): Whether the OS sets the DF bit on the intial packet. 