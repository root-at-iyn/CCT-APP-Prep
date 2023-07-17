# Domain Reconnaissance

## Identifying domains/workgroups and domain membership within the target network.

## Identifying key servers within the target domains.

## Identifying and analysing internal browse lists.

## Identifying and analysing accessible SMB shares

From Pentestdairy: http://pentestdiary.blogspot.com/2017/08/crest-cct-application-exam.html
- protocol used to access and share resources
    - runs over NetBIOS over TCP/IP (port 139)
    - runs over TCP/IP directly (port 445)
    - RPCs available through IPC$ (Inter-Process Connection shared areas)
    - SMB session is authenticated
- Null Sessions
    - SMB session with no credentials (blank username and password)
    - Some RPCs provide information with just a null session
    - Required for legacy Windows systems
    - Requirement gradually phased out
    - Domain Controllers are often more obliging (200/2003).
    - net use \\ipaddress\ipc$ /u:"" ""
- Domains
    - net user /domain ---- a list of domain groups is returned
    - net group /domain --- a list of domain groups is returned
    - net user blabla /domain ---- details of the "blabla" user account are returned
    - rundll32 dsquery,OpenQueryWindow ---- active directory searches
