# Law & Compliance

## UK laws important to Information Security

### Computer Misuse Act 1990

- Ref: [Computer Misuse Act 1990
](https://www.legislation.gov.uk/ukpga/1990/18/contents)
    1. [Unauthorised access to computer material.](https://www.legislation.gov.uk/ukpga/1990/18/section/1)
        - **A person is guilty of an offense if**:
            1. he causes a computer to perform any function with intent to secure access to any program or data held in any computer [or to enable any such access to be secured];
            2. the access he intends to secure [or to enable to be secured,] is unauthorised; and
            3. he knows at the time when he causes the computer to perform the function that that is the case.
    2. [Unauthorised access with intent to commit or facilitate commission of further offences.](https://www.legislation.gov.uk/ukpga/1990/18/section/2)
    3. [Unauthorised acts with intent to impair, or with recklessness as to impairing, operation of computer, etc.](https://www.legislation.gov.uk/ukpga/1990/18/section/3)
        - **A person is guilty of an offence if**:
            1. he does any unauthorised act in relation to a computer;
            2. at the time when he does the act he knows that it is unauthorised; and
            3. either subsection (2) or subsection (3) below applies
        - **This subsection applies if the person intends by doing the act**:
            1. to impair the operation of any computer;
            2. to prevent or hinder access to any program or data held in any computer;
            3. to impair the operation of any such program or the reliability of any such data;
            4. to enable any of the things mentioned in paragraphs (a) to (c) above to be done.

### Human Rights Act 1998

- Ref: [The Articles](https://www.legislation.gov.uk/ukpga/1998/42/schedule/1)

- **NOTE:** Only Article 8 is relevant to Pentetration testing

- __Right to respect for private and family life__
    1. Everyone has the right to respect for his private and family life, his home and his correspondence.
    2. There shall be no interference by a public authority with the exercise of this right except such as is in accordance with the law and is necessary in a democratic society in the interests of national security, public safety or the economic well-being of the country, for the prevention of disorder or crime, for the protection of health or morals, or for the protection of the rights and freedoms of others.


### Data Protection Act 1998

- Ref: [Data Protection Act 1998](https://www.legislation.gov.uk/ukpga/1998/29/contents)
- **NOTE:** This was superseded by [Data Protection Act 2018](https://www.legislation.gov.uk/ukpga/2018/12/contents)

### Police and Justice Act 2006

- **NOTE:** The part relevant to penetration testing is [Computer Misuse](https://www.legislation.gov.uk/ukpga/2006/48/part/5/crossheading/computer-misuse)
- **Repeals and amendments:** [Serious Crime Act 2007 Section 61](https://www.legislation.gov.uk/ukpga/2007/27/section/61#section-61-2)

## Law impact to Penetration Testing

The law can affect penetration testing activies in multiple ways. Relevative to each law, these are:

### Computer Misuse Act 1990

- Testing systems that are out of scope. By testing a system that is out of the scope of the test, you are effectively attempting to gain access to an unauthorised system.
- Performing or causing a denial of service without authorisation from the client. 
- Producing exploit code intended for a test target, but is copied or obtained by another party who uses it on an unathorised system. You would still be liable here.

### Human Rights Act 1998

- Tools like packet sniffers could violate this law if personal data from employees or the organisation's clients have been captured. 

### Data Protection Act 1998 (2018)

- Packet sniffers and personal data capturing would also apply here. 
- Testing a live system with customer data and obtaining customer records. In this scenario, the customer would not have authroised their data to be processed in this manner, so it would violate the DPA.

## Sector-specific regulatory issues

## Financial Services
### PCI-DSS
- Ref: [Penetration Testing Guidance (Requirement 11.3)](https://listings.pcisecuritystandards.org/documents/Penetration_Testing_Guidance_March_2015.pdf)
- Requires testing to be performed twice a year, or when a major change in the environment occurs

## Standards
### ISO 27001
- **Control Objective A12.6 (Technical Vulnerability Management)**
    - *information about technical vulnerabilities of information systems being used shall be obtained in a timely fashion, **the organisation's exposure to such vulnerabilities evaluated** and appropriate measures taken to address the associated risk*