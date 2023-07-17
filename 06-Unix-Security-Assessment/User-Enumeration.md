# User Enumeration

## Discovery of valid usernames from network services commonly running by default:
### - rusers
### - rwho
### - SMTP
### - finger

### User Enum
Ref: http://pentestdiary.blogspot.com/2017/08/crest-cct-application-exam.html
- enum4linux -U -u "username" -p "pass" -a ipadd


## Understand how finger daemon derives the information that it returns, and hence how it can be abused.
Ref: http://pentestdiary.blogspot.com/2017/08/crest-cct-application-exam.html

- Finger Protocol is used for the exchange of human-oriented status and user information. Runs on port 79; Finger works by querying entries in the passwd files, i.e. GECOS fields. Finger can also be used to query "plan" files. Plan files can be created by users to inform others of their current activity,humour or anything else that the user may wish to share. this prot. soffers from the vulnerabilities "CVE-2001-1503 Solaris information Disclousre vulnerability", in which an atacker can list all the users of a host by requesting: finger 'a b c d e f g h'@target.com

    - open terminal window (Windows OS is the client or use Kali but need to download packages) and type ```finger root@IPaddress``` to see if root is a valid account username in the target host
    - to automate the user enumeration process run: 

    ```for i in $(cat /mnt/host/Wordlist/users.txt); do finger $i@ipaddress | grep "Login"; done```

    - to automate the plan enumeration process run: 
    
    ```for i in $(cat /mnt/host/Wordlist/users.txt); do finger $i@ipaddress | grep -a2 "Plan:"; done```

    - -a2 prints two lines after a match is found