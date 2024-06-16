# Host Enumeration

## Port Scanning

## Service Enumeration

## OS Fingerprinting

### Manual OS Fingerprinting

### Automated OS Fingerprinting

## Banner Grabbing

## Curl
```
curl -IL http://10.0.0.2
```
## Wget

## Telnet

## PowerShell

## Python

# Traffic Analysis

## Packet Capture

### Tcpdump
*View bytes in hex and ASCII with segment size of 65535 (bytes)*
```
sudo tcpdump -i en0 -s 65535 -X
```
*Capture traffic on port 80 and Automatically decodes bytes to ASCII*
```
sudo tcpdump -i en0  -A port 80
```

### Wireshark

### Tshark

### Scapy

# Application Content Mapping

## Manual Application Content Mapping

## Automated Application Content Mapping

# Application Analysis

## Application Analysis

### Identifying Functionality

### Identifying Data Entry Points

### Identifying Technology Used

### Attack Surface Mapping
