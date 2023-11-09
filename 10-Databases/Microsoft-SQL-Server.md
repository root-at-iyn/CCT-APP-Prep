# Microsoft SQL Server

## Knowledge of common attack vectors for Microsoft SQL Server.

### Enumeration

- The SQL Server process `sqlservr.exe` by default listens on TCP port **1433**.
- **Microsoft SQL Monitor** provides information about the SQL Server and any instances, by responding to a single byte query packet with the value `0x02`. The SQL Monitor service listens on UDP port **1434**.
- The SQLPing utility (and nmap scripts) can be used gather information about the SQL Serevr such as:
    - Server name
    - Instance name
    - If the server is part of a cluster
    - Named Pipes
    - TCP port of the running sqlservr.exe process
    - SQL Server version installed
- SQL Server can also run in *hidden mode*, which moves the default `sqlservr.exe` port to **2433**.

### Authentication and Authorization

*TODO*

### Dangerous Stored Procedures

| Stored Procedure | Abuse case |
|------------------|------------|
|xp_cmdshell       | Run OS commands as NT AUTHORITY\SYSTEM|
|xp_displayparamstmt| ? |
|xp_execresultset|?|
|xp_instance_regaddmultistring|?|
|xp_instance_regdeletekey|?|
|xp_instance_regdeletevalue|?|
|xp_instance_regenumvalues|?|
|xp_instance_regread|?|
|xp_instance_regwrite|?|
|xp_regaddmultistring|?|
|xp_regdeletekey|?|
|xp_regdeletevalue|?|
|xp_regenumvalues|?|
|xp_regread|?|
|xp_regremovemultistring|?|
|xp_regwrite|?|
|sp_OACreate|?|
|sp_OADestroy|?|
|sp_OAGetErrorInfo|?|
|sp_OAGetProperty|?|
|sp_OAMethod|?|
|sp_OASetProperty|?|
|sp_OAStop|?|

:exclamation: Stored Procedures that are not required should be removed:

```sql
exec sp_dropextendedproc 'xp_cmdshell'
```
Where this is not possible, privileges should be revoked from all users of the database except `sysadmin`. The `public` role should not have permissions:

```sql
revoke execute on xp_instance_regread to public
```
Low priv users also should not be able to manage SQL Server Agent jobs. Privileges should be removed on the following stored procedures:

- sp_add_job
- sp_add_jobstep
- sp_add_jobserver
- sp_start_job

## Understanding of privilege escalation and attack techniques for a system compromised via database connections.

