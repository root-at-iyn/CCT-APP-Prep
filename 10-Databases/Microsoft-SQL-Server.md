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

MS SQL Server supports two modes of authentication:

- Native SQL Server Authentication
    - When using Native SQL authentication, the password is obfuscated before being sent to the server.
    - The obfuscated password is easily reverseable (in earlier versions) because:
        - every other byte is set to `0xA5`
        - the password string is converted to unicode and then the first 4 bytes swapped around
        - the password output is then `XOR` with `0xA5`
- Windows Authentication
    - The user's login must map to a Windows user or group within the same administrative domain/network as the SQL Server. 
    - Windows authentication uses tokens that reference the Windows Security Identifier (`SID`), which is compared against the sysxlogins table.

- Login creds (username and passwd hash) are stored in the **master database** `sysxlogins` table.

:exclamation: Windows Authentication should be used in favour of Native SQL due to the security issues with password obfuscation, and the risk of the default and well known `sa` account being targeted.


- The SQL Server authentication mode is set in the following registry keys:

| Registry Key | Windows Authentication | Native Authentication |
|--------------|------------------------|-----------------------|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\MSSQLServer\LoginMode| 1|2|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\[Instance]\LoginMode| 1|2|

The following code changes the authentication from mixed mode (Windows and Native) to just Windows only:

```sql
USE [master]
GO
EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE',
     N'Software\Microsoft\MSSQLServer\MSSQLServer',
     N'LoginMode', REG_DWORD, 1;
GO
```


### OPENROWSET Re-Authentication

Low-priv users can re-authenticate with SQL Server if the have access to the `OPENROWSET` command. This is typically used to get data from a remote `OLE DB` daat source.

*example: OLE DB Provider for ODBC (MSDASQL)*

```sql
select * from OPENROWSET('MSDASQL', 'DRIVER=(SQL Server);SERVER=;uid=sa;pwd=password', 'select @@version')
```

*example: OLE DB Provider for SQL Server (SQLOLEDB)*

```sql
select * from OPENROWSET('SQLOLEDB', '', 'sa', 'paswword', 'select @@version')
```
- By default in SQL Server 2000, low priv users cannit execute using `MSDASQL`, but they can using `SQLOLEDB` syntax. 
- This allowed user accounts to be brute-forced in early versions of SQL Server 2000, since invalid OPENROWSET commands leaked account names in error messages.
- OPENROWSET command can also be used to read from Microsoft Excel files and Microsoft Access database files. 
- Using OPENROWSET with SQLOLEDB in this way is known as ad-hoc queries and can by disbaled by setting the registry value **DisallowAdhocAccess** to 1 on the key: `HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLSERVER\Providers\[Provider name]` 

### Dangerous Stored Procedures

| Stored Procedure | Abuse case |
|------------------|------------|
|xp_cmdshell       | Run OS commands as NT AUTHORITY\SYSTEM|
|xp_displayparamstmt| ? |
|xp_execresultset|When using Windows AuthN, can cause the SQL server to reconnect to itself and bypass access controls|
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

### Uploading Files

*TODO*

## Understanding of privilege escalation and attack techniques for a system compromised via database connections.

