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

