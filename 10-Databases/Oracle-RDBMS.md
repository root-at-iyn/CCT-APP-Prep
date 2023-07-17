# Oracle RDBMS

## Derivation of version and patch information from hosts running Oracle software.

## Default Oracle accounts.

- SYSADMIN
- SYS
- SYSTEM
- DBSNMP
- OUTLN

### Known default creds

| Account | Password|
| --------| --------|
|SYS |	CHANGE_ON_INSTALL|
|SYS |	SYSPASS|
|SYS |	SYS|
|SYSADM|	SYSADM|
|SYSADMIN|	SYSADMIN|
|SYSMAN|	OEM_TEMP|
|SYSTEM|	MANAGER|
|SYSMAN|	SYSMAN|
|SYSTEM|	SYSTEMPASS|

### Enumerating the Oracle DB

- Looking in SYS.LINK$ table for passwords		
- Trying to collect a list of users from the SYS.ALL_USERS table		
- Trying to collect a list of old password hashes from SYS.USER_HISTORY$		
- Trying to collect a list of accounts and password hashes from the SYS.USER$ table		
- Trying to collect a list of users and password hashes from the DBA_USER view		
- Trying to collect info on profiles from DBA_PROFILES		
- Trying to collect info on parameters from V$PARAMETER		
- Trying to collect a list of accounts and possible passwords from the SYS.AUD$ table		

## Useful Links

- https://www.rapid7.com/db/vulnerabilities/oracle-default-account-sysadmin/#:~:text=ORACLE%20creates%20a%20default%20account,level%20access%20to%20the%20system.
- http://www.petefinnigan.com/default/default_password_list.htm
- https://docs.oracle.com/cd/E11882_01/server.112/e10575/tdpsg_user_accounts.htm#TDPSG20000

