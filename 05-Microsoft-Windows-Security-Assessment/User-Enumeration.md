# User Enumeration

## Identifying user accounts on target systems and domains using:
### - NetBIOS

### - SNMP
- snmpwalk -c public -v1 192.168.1.1 1.3.6.1.4.1.77.1.2.25 (windows users accounts)
- community string bruteforce: onesixtyone -c dictionary host
### - LDAP

## Useful Links
- Enuemrate Users and Groups: https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#enumerate-users-and-groups