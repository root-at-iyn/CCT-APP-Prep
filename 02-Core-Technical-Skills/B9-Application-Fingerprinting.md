# Application Fingerprinting and Evaluating Unknown Services

## Determining server types and network application versions from application banners.

*From Wikapedia:*
>Banner grabbing is a technique used to gain information about a computer system on a network and the services running on its open ports. Administrators can use this to take inventory of the systems and services on their network. However, an intruder can use banner grabbing in order to find network hosts that are running versions of applications and operating systems with known exploits.


This can be done via multiple tools. An application framework or web server typically has its name a version within the banner if default configuration is unmodified. This may appear as;
- X Powered by {Framework Name}
- Apache {X.x.x}
- Nginx {X.x.x}
- IIS {x.x}

*where x is the version of the web server software*

This is not restricted to web servers or application frameworks, but can also appear in TCP based server software, such as: 
- SSH
- FTP
- ESMTP

For more on banner grabbing, see [Multiple Ways to Banner Grabbing](https://www.hackingarticles.in/multiple-ways-to-banner-grabbing/) and Wikapedia's definition [Banner Grabbing](https://en.wikipedia.org/wiki/Banner_grabbing)

## Evaluation of responsive but unknown network applications.

Enumeration unkown services is can be done via: 
 - **Nmap**: If Nmap or other port scanning tool shows there is an open TCP/UDP port, you can try running a service scan with the `-V` argument. NMAP will send probes and try to identity the service based on signature patterns. 
 - **Port Independent Detection**: Port Independent Detection is a technique of identifying network services by statistical analysis of the `protocol`, `session behaviour`, `packet sizes` and `payload data`. This technique is also used in Network Intrusion Detection Frameworks. For example, you can compare the IP `TTL`, `TCP Window Sizes` and responses to malformed packets.

 - Ref: 
    - https://www.icir.org/robin/papers/usenix06/
    - https://www.netresec.com/?page=Blog&month=2015-10&post=Port-Independent-Protocol-Detection
