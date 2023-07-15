# Understanding Explaining and Managing Risk

## Knowledge of additional risks that penetration testing can present
- Outages
    - During the testing phase, a tester could accidently cause a system to stop working, causing an outage if testing in a live production environment.
- Compromise
    - If systems are modified during a peentration test, such as the tester creating a backdoor into the network or changing an access control, forgetting to revert the configuration could leave the system vulnerable to attack.
    - Exploit scripts from the test being left within the target environment or host. The could be also be used by a malicious actor.
- Information Disclosure
    - The potential for test findings being shared to unauthorised personel.
- Unauthorised Testing
    - Incorrect target scope leading to testing unauthorised systems.

## Levels of risk relating to penetration testing, the usual outcomes of such risks materialising and how to mitigate the risks

- Covered in the points above and below.

## Effective planning for potential DoS conditions

- Check during scoping for systems sensitive to network scans or high levels of I/O.
- Exclude the sensitive / unstable systems from automated scanning.
- Ensure there are backups of the system and databases before testing.
- Limit the concurrency of network and vulnerability scans.
- Avoid exploit payloads that could cause a risk of denial of service.