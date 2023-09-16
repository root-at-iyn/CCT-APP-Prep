# IPSec

## Enumeration and fingerprinting of devices running IPSec services.

Ike-Scan is trypically used to enumerate and fingerprint IPSec services. See https://www.kali.org/tools/ike-scan/ and https://github.com/royhills/ike-scan for more info.

We can eumerate / fingerprint the IPSec service by: 
- **Backoff fingerprinting**: ike-scan allows us to obtain the backoff pattern from a VPN server, and it will also try to match the pattern received against a database of known patterns. This will guess the implementation (transform sets) and device (vendor) based on the pattern.
- **Brute Forcing the group (ID)** in IKE Agressive mode scans.
- **Obtaining a PSK Hash** using Agressive mode scans with an enumerated group
- **Cracking the PSK** using psk-crack
- **Obtain XAUTH credentials** by MitM attack when a group and secret key are known.

Ref: 
- https://www.royhills.co.uk/wiki/index.php/Ike-scan_User_Guide
- https://book.hacktricks.xyz/network-services-pentesting/ipsec-ike-vpn-pentesting#capturing-and-cracking-the-hash