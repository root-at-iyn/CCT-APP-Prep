# Active Directory

## Active Directory Roles (Global Catalogue, Master Browser, FSMO)

### Global Catalogue
Ref: [Global Catalogue](https://learn.microsoft.com/en-us/windows/win32/ad/global-catalog)
- The `global catalog` contains a replica of all of the directory objects for an entire forest. The global catalog only contains a subset of the attributes for each object.
- A `global catalogue server` is a domain controller that contains the global catalog for the forest.

### Master Browser
Ref: [Master Browser Server](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-brws/8e18326b-26a2-4790-a914-d69f64250eb4)
- A server that is responsible for `maintaining a master list of available resources on a subnet` and for making the list available to backup browser servers. Each subnet requires a master browser server. The master browser server for a particular domain is called the domain master browser server.


### Single-Master-Operations (FSMO)
Ref: [Active Directory FSMO roles in Windows](https://learn.microsoft.com/en-us/troubleshoot/windows-server/identity/fsmo-roles)

To prevent conflicting updates in Windows, the Active Directory performs updates to certain objects in a single-master fashion. In a single-master model, only one DC in the entire directory is allowed to process updates. It's similar to the role given to a primary domain controller (PDC) in earlier versions of Windows, such as Microsoft Windows NT 3.51 and 4.0. In earlier versions of Windows, the PDC is responsible for processing all updates in a given domain.

Active Directory extends the single-master model found in earlier versions of Windows to include multiple roles, and the ability to transfer roles to any DC in the enterprise. Because an Active Directory role isn't bound to a single DC, it's referred to as an FSMO role. Currently in Windows there are five FSMO roles:

- Schema master
- Domain naming master
- RID master
- PDC emulator
- Infrastructure master

Typically, an FSMO role ownership is executed only when the domain controller has replicated the naming context (NC) where the ownership is stored since the Directory Service started. Make sure that an FSMO role seizure reaches the previous owner before the role is used. 

## Reliance of AD on DNS and LDAP

Ref: [DNS and AD DS](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/dns-and-ad-ds)


## Group Policy (Local Security Policy)
- Ref: [About Group Policy API](https://learn.microsoft.com/en-us/previous-versions/windows/desktop/policy/about-group-policy)
- Ref: [Security policy settings](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/security-policy-settings#policy-based-security-settings-management)
- Ref: [Local Security Policy](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/administer-security-policy-settings#local-security-policy)
- Ref: [Using the Local Security Policy snap-in](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/administer-security-policy-settings#using-the-local-security-policy-snap-in)

