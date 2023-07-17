# Exchange

## Knowledge of common attack vectors for Microsoft Exchange Server.

### Exchange Overview
Microsoft Exchange Server is a mail server which acts as a Mail Transfer Agent (MTA). It supports email protocols such as SMTP, POP, IMAP, and also includes web services such as Outlook Web Access and Exchange Web Services (EWS). All of this fucntionality can be considered attack surface, since these services are internet facing.

### Common Attacks

Generally, Microsoft Exchange is susceptible to the following attack vectors:
- Password Spraying
- User Enuemration (via EWS. This can bypass MFA requirements)
- Attacks on POP / IMAP / SMTP (When POP and IMAP is enabled you also bypass MFA)

### Vulnerabilities 

- ProxyLogon
- ProxyShell
- WebShell Uploads

### Useful Links
- https://github.com/kh4sh3i/exchange-penetration-testing
- https://www.microsoft.com/en-us/security/blog/2021/03/25/analyzing-attacks-taking-advantage-of-the-exchange-server-vulnerabilities/
- https://pentestlab.blog/2019/09/16/microsoft-exchange-privilege-escalation/