# Windows Vulnerabilities

## Knowledge of remote windows vulnerabilities, particularly those for which robust exploit code exists in the public domain.

Can search for these in vulnerability databases: 
- http://pentestdiary.blogspot.com/2017/08/public-vulnerability-database-resources.html

## Knowledge of local windows privilege escalation vulnerabilities and techniques.
- https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation

## Knowledge of common post exploitation activities:

### - Obtain password hashes, both from the local SAM and cached credentials
- https://book.hacktricks.xyz/windows-hardening/stealing-credentials#stealing-sam-and-system
- https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#cached-credentials
- https://www.onlinehashcrack.com/how-to-extract-crack-LSA-cached-credentials.php
- https://www.ampliasecurity.com/research/wce12_uba_ampliasecurity_eng.pdf

### - Obtaining locally-stored clear-text passwords
- Stealing Windows Credentials: https://book.hacktricks.xyz/windows-hardening/stealing-credentials
- Finding Passwords in SYSVOL and Group Policy Preferences: https://adsecurity.org/?p=2288

### - Crack password hashes
- https://book.hacktricks.xyz/generic-methodologies-and-resources/brute-force#ntlm-cracking

### - Check patch levels
- https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#system-info

### - Derive list of missing security patches
- https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#system-info

### - Reversion to previous state

