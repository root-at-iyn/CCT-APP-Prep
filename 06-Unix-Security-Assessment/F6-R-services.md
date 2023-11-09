# R* services

## Berkeley r* service:
### - Access control (/etc/hosts.equiv and .rhosts) trust relationships
### - Impact of poorly-configured trust relationships.

#### Overview

- The **/etc/hosts.equiv** and **~/.rhosts** files provide the **remote authentication** database for the rcmd function and the following commands: 
    - **lpd**
    - **rcp**
    - **rlogin**
    - **rsh** 
- These files **bypass the standard password-based user authentication mechanism**. 
- They specify remote hosts and users that are considered trusted (i.e. are allowed to access the local system without supplying a password):

#### Permission Scope
- on a system-wide basis (/etc/hosts.equiv)
- by an individual user (~/.rhosts).

- Ref: https://www.qnx.com/developers/docs/6.5.0SP1.update/com.qnx.doc.neutrino_utilities/h/hosts.equiv.html

Use extreme caution in `/etc/hosts.equiv` with positive entries that include a username field (either an individual named user, a netgroup, or `+` sign). 

:exclamation: Because `/etc/hosts.equiv` applies `system-wide`, these entries allow one or a group of remote users to access the system as any local user without providing a password. This can be a security hole.