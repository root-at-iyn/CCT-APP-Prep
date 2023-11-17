# Interpretting Tool Output

## Interpreting output from port scanners, network sniffers and other network enumeration tools.

### Nmap Port Scan
Ref: https://nmap.org/book/man-examples.html 

*TCP Scan with version detection*

>Launches host enumeration and a TCP scan at the first half of each of the 255 possible eight-bit subnets in the 198.116.0.0/16 address space. This tests whether the systems run SSH, DNS, POP3, or IMAP on their standard ports, or anything on port 4564. For any of these ports found open, version detection is used to determine what application is running.
```
nmap -sV -p 22,53,110,143,4564 198.116.0-255.1-127
```
A `SYN` scan *(sending a TCP SYN packet )* could be used by replacing `-sV` for `-sSV`. A SYN scan requires root privileges.

### TCPDUMP

Ref: https://hackertarget.com/tcpdump-examples/ 

*Captures all traffic in verbose mode to TCP port 80 from network interface eth0*

```bash
sudo tcpdump -i eth0 -nn -s0 -v port 80
```
- **-i** : Select interface that the capture is to take place on, this will often be an ethernet card or wireless adapter but could also be a vlan or something more unusual. Not always required if there is only one network adapter.
- **-nn** : A single (n) will not resolve hostnames. A double (nn) will not resolve hostnames or ports. This is handy for not only viewing the IP / port numbers but also when capturing a large amount of data, as the name resolution will slow down the capture.
- **-s0** : Snap length, is the size of the packet to capture. -s0 will set the size to unlimited - use this if you want to capture all the traffic. Needed if you want to pull binaries / files from network traffic.
- **-v** : Verbose, using (-v) or (-vv) increases the amount of detail shown in the output, often showing more protocol specific information.
port 80 : this is a common port filter to capture only traffic on port 80, that is of course usually HTTP.


*Captures all packets on default interface, shows ASCII Text, line buffers output, and pipes to grep to find `pwd`, `passwd`, `password` or `Host`*

```bash
tcpdump -s 0 -A -n -l | egrep -i "POST /|pwd=|passwd=|password=|Host:"
```
```powershell
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on enp7s0, link-type EN10MB (Ethernet), capture size 262144 bytes
11:25:54.799014 IP 10.10.1.30.39224 > 10.10.1.125.80: Flags [P.], seq 1458768667:1458770008, ack 2440130792, win 704, options [nop,nop,TS val 461552632 ecr 208900561], length 1341: HTTP: POST /wp-login.php HTTP/1.1
.....s..POST /wp-login.php HTTP/1.1
Host: dev.example.com
.....s..log=admin&pwd=notmypassword&wp-submit=Log+In&redirect_to=http%3A%2F%2Fdev.example.com%2Fwp-admin%2F&testcookie=1
```

