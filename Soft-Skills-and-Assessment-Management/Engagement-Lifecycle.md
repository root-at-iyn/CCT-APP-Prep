# Engagement Lifecycle

Since this exam is used to meet NCSC approved testing guidelines, you'll find most of the Soft Skills and Assessment details on the NCSC site. The following text has been taken from [Penetration Testing](https://www.ncsc.gov.uk/guidance/penetration-testing)

## Benefits and utility of penetration testing to the client

Penetration testing should be viewed as a method for gaining assurance in your organisation's vulnerability assessment and management processes, not as a primary method for identifying vulnerabilities.

### Assurance of configuration and security controls

A well-scoped penetration test can give `confidence that the products and security controls tested have been configured in accordance with good practice` and that there are `no common or publicly known vulnerabilities` in the tested components, at the time of the test.

## Structure of penetration testing, including the relevant processes and procedures

### Initital engagement
- Ensure that the external team has the relevant qualifications and skills to perform testing on your IT estate.
- If you have any unusual systems (mainframes, uncommon networking protocols, bespoke hardware etc.) these should be highlighted in the bid process so that the external teams know what skill sets will be required.

### Scoping

- Scoping a penetration test should involve:
    1. All relevant risk owners
    2. Technical staff knowledgeable about the target system
    3. A representative of the penetration test team

- Special requirements
    - During scoping, you should outline any issues which might impact on testing. This might include the need for out-of-hours testing, any critical systems where special handling restrictions are required, or other issues specific to your organisation.
- Scoping document output
    1. The technical boundaries of the test
    2. The types of test expected
    3. The timeframe and the amount of effort necessary to deliver the testing (usually given in terms of resource days)
    4. Depending on the type of approach agreed, this document may also contain a number of scenarios or specific 'use cases' to test
    5. The penetration testing team's requirements. This will allow you to do any necessary preparation before the date of the test. For example, by creating test accounts or simply allocating desk space
    6. Any compliance or legislative requirements that the testing plan must meet
    7. Any specific reporting requirements, for example the inclusion of CVSS scores or use of CHECK severity levels
    8. Any specific time constraints on testing or reporting, that a penetration testing company will need to consider when allocating resources

### Testing
- Communicaton
    - Ensure that a technical point of contact is available at all times
- Caution
    - The testers should make every effort to avoid causing undue impact to the system being tested
- Scope change
    - The testing team may identify additional systems or components which lie outside of the testing scope but have a potential impact on the security of the system(s) which have been defined as in scope. The testing team can either request a change of scope to include the item, or record the exclusion of the item as a limitation of the test. The risk owner will be the decision maker whether to include / exclude

### Reporting

The report should include:
- Any security issues uncovered
- An assessment by the test team as to the level of risk that each vulnerability exposes the organisation or system to
- A method of resolving each issue found
- An opinion on the accuracy of your organisation's vulnerability assessment
- Advice on how to improve your internal vulnerability assessment process 

### Severity rating

- The [Common Vulnerability Scoring System](https://www.first.org/cvss) gives a numerical score identifying the severity of a vulnerability
- CHECK reports are required to state the level of risk as HIGH, MEDIUM, LOW or INFORMATIONAL in descending order of criticality
- For CHECK reports, scoring systems such as CVSS may be used in addition to (but not in place of) this
- Ratings can be changed in the case of mitigations that limit the effectiveness of a vulnerability
- Any deviation from associating a vulnerability with its standard rating should be documented and justified by the penetration testing team

### Follow up
- The penetration test report should be assessed by the organisation's vulnerability management group in a similar manner to the results of an internal vulnerability assessment
- Risk assessment and decisions on the application of fixes are the organisation's responsibility
- The test team may not have had access to all details about a specific system or the potential business impact of the exploitation of a vulnerability. Consequently, they may rate issues lower or higher than the organisation's internal team. The organisation should review the issues and identify the risks relative to their environment.

## Concepts of infrastructure testing and application testing, including black box and white box formats

### Blackbox testing

- No information is shared with the testers about the internals of the target. This type of testing is performed from an external perspective and is aimed at identifying ways to access an organisation's internal IT assets. This more accurately models the risk faced from attackers that are unknown or unaffiliated to the target organisation. However, the lack of information can also result in vulnerabilities remaining undiscovered in the time allocated for testing.

### Whitebox testing

- Full information about the target is shared with the testers. This type of testing confirms the efficacy of internal vulnerability assessment and management controls by identifying the existence of known software vulnerabilities and common misconfigurations in an organisation's systems.

### Infrastructure testing

- As the name suggests, infrastructure testing focuses on testing an organisation's infrastructure, including systems and network services. This can be broken down into Internal (non-internet facing) and External (internet facing) assets. For example: 
    - External
        - Mail Servers
        - Web Apps
        - Firewalls
        - Proxies
        - Voip Services
        - File Servers
    - Internal
        - Network Services (LDAP, SMB, SNMP, SMTP, FTP, HTTP, RPC, NetBIOS, NFS, SSH)
        - Authentication Services (Kerberos, NTLM)
        - Active Directory Servers
        - File Servers / Shares
        - Database Servers
        - Internal Web Apps
        - Firewalls / Routers / Switches
        - Voip Servers

### Application Testing

- Focuses on testing web applications and web services.

## Project closure and debrief

- The assessment should be completed, with finalised risk ratings for all issues. 
- The report should be written with an executive summary of the testing, a summary of all issues found in the test, and detailed explanations of the issues found.
- The report should be delivered to the organisation by the test team, offering a debrief call to explain the results.

- From the organisations perspective, this has already been discussed in [Follow up](./Engagement-Lifecycle.md#follow-up)