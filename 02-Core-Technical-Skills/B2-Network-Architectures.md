# Network Architectures

## Cat 5 / Fibre

- Ref: https://en.wikipedia.org/wiki/Category_5_cable
- Ref: https://www.techjunkie.com/ethernet-vs-fiber-optic-cables/#:~:text=While%20this%20is%20lightning%20fast,four%20pairs%20inside%20the%20cable.

## 10/100/1000baseT
- Ref: https://en.wikipedia.org/wiki/Gigabit_Ethernet

## Token ring
- Ref: https://en.wikipedia.org/wiki/Token_Ring

## Wireless (802.11)

### Overview

### Security

- Copy paste from Wikapedia
- Ref: https://en.wikipedia.org/wiki/IEEE_802.11#Security

> In 2001, a group from the University of California, Berkeley presented a paper describing weaknesses in the 802.11 Wired Equivalent Privacy (WEP) security mechanism defined in the original standard; they were followed by Fluhrer, Mantin, and Shamir's paper titled "Weaknesses in the Key Scheduling Algorithm of RC4". Not long after, Adam Stubblefield and AT&T publicly announced the first verification of the attack. In the attack, they were able to intercept transmissions and gain unauthorized access to wireless networks.

> The IEEE set up a dedicated task group to create a replacement security solution, 802.11i (previously, this work was handled as part of a broader 802.11e effort to enhance the MAC layer). The Wi-Fi Alliance announced an interim specification called Wi-Fi Protected Access (WPA) based on a subset of the then-current IEEE 802.11i draft. These started to appear in products in mid-2003. IEEE 802.11i (also known as WPA2) itself was ratified in June 2004, and uses the Advanced Encryption Standard (AES), instead of RC4, which was used in WEP. The modern recommended encryption for the home/consumer space is WPA2 (AES Pre-Shared Key), and for the enterprise space is WPA2 along with a RADIUS authentication server (or another type of authentication server) and a strong authentication method such as EAP-TLS.[citation needed]

> In January 2005, the IEEE set up yet another task group "w" to protect management and broadcast frames, which previously were sent unsecured. Its standard was published in 2009.

> In December 2011, a security flaw was revealed that affects some wireless routers with a specific implementation of the optional Wi-Fi Protected Setup (WPS) feature. While WPS is not a part of 802.11, the flaw allows an attacker within the range of the wireless router to recover the WPS PIN and, with it, the router's 802.11i password in a few hours.

> Wi-Fi users may be subjected to a Wi-Fi deauthentication attack to eavesdrop, attack passwords, or force the use of another, usually more expensive access point.

## Security implications of shared media, switched media and VLANs

### Shared Media

- Copy paste from Wikapedia
- Ref: https://en.wikipedia.org/wiki/IEEE_802.1X#Shared_media

> In the summer of 2005, Microsoft's Steve Riley posted an article (based on the original research of Microsoft MVP Svyatoslav Pidgorny) detailing a serious vulnerability in the 802.1X protocol, involving a man in the middle attack. In summary, the flaw stems from the fact that 802.1X authenticates only at the beginning of the connection, but after that authentication, it's possible for an attacker to use the authenticated port if he has the ability to physically insert himself (perhaps using a workgroup hub) between the authenticated computer and the port. Riley suggests that for wired networks the use of IPsec or a combination of IPsec and 802.1X would be more secure.

> EAPOL-Logoff frames transmitted by the 802.1X supplicant are sent in the clear and contain no data derived from the credential exchange that initially authenticated the client. They are therefore trivially easy to spoof on shared media and can be used as part of a targeted DoS on both wired and wireless LANs. In an EAPOL-Logoff attack a malicious third party, with access to the medium the authenticator is attached to, repeatedly sends forged EAPOL-Logoff frames from the target device's MAC Address. The authenticator (believing that the targeted device wishes to end its authentication session) closes the target's authentication session, blocking traffic ingressing from the target, denying it access to the network.

> The 802.1X-2010 specification, which began as 802.1af, addresses vulnerabilities in previous 802.1X specifications, by using MACsec IEEE 802.1AE to encrypt data between logical ports (running on top of a physical port) and IEEE 802.1AR (Secure Device Identity / DevID) authenticated devices.

> As a stopgap, until these enhancements are widely implemented, some vendors have extended the 802.1X-2001 and 802.1X-2004 protocol, allowing multiple concurrent authentication sessions to occur on a single port. While this prevents traffic from devices with unauthenticated MAC addresses ingressing on an 802.1X authenticated port, it will not stop a malicious device snooping on traffic from an authenticated device and provides no protection against MAC spoofing, or EAPOL-Logoff attacks.

### Switched Media

### VLANs

- Copy paste from Wikapedia
- Ref: 

> VLAN hopping is a computer security exploit, a method of attacking networked resources on a virtual LAN (VLAN). The basic concept behind all VLAN hopping attacks is for an attacking host on a VLAN to gain access to traffic on other VLANs that would normally not be accessible. There are two primary methods of VLAN hopping: switch spoofing and double tagging. Both attack vectors can be mitigated with proper switch port configuration.

> Switch spoofing
In a switch spoofing attack, an attacking host imitates a trunking switch by speaking the tagging and trunking protocols (e.g. Multiple VLAN Registration Protocol, IEEE 802.1Q, Dynamic Trunking Protocol) used in maintaining a VLAN. Traffic for multiple VLANs is then accessible to the attacking host.

> Mitigation
Switch spoofing can only be exploited when interfaces are set to negotiate a trunk. To prevent this attack on Cisco IOS, use one of the following methods 

> 1. Ensure that ports are not set to negotiate trunks automatically by disabling DTP:

`Switch (config-if)# switchport nonegotiate`

> 2. Ensure that ports that are not meant to be trunks are explicitly configured as access ports

`Switch (config-if)# switchport mode access`

>Double tagging
In a double tagging attack, an attacker connected to an 802.1Q-enabled port prepends two VLAN tags to a frame that it transmits. The frame (externally tagged with VLAN ID that the attacker's port is really a member of) is forwarded without the first tag because it is the native VLAN of a trunk interface. The second tag is then visible to the second switch that the frame encounters. This second VLAN tag indicates that the frame is destined for a target host on a second switch. The frame is then sent to the target host as though it originated on the target VLAN, effectively bypassing the network mechanisms that logically isolate VLANs from one another. However, possible replies are not forwarded to the attacking host (unidirectional flow).

>Mitigation
Double Tagging can only be exploited on switch ports configured to use native VLANs.  Trunk ports configured with a native VLAN don't apply a VLAN tag when sending these frames. This allows an attacker's fake VLAN tag to be read by the next switch.

> Double Tagging can be mitigated by any of the following actions (Incl. IOS example):

>Simply do not put any hosts on VLAN 1 (The default VLAN). i.e., assign an access VLAN other than VLAN 1 to every access port
 
 `Switch (config-if)# switchport access vlan 2`

>Change the native VLAN on all trunk ports to an unused VLAN ID.

`Switch (config-if)# switchport trunk native vlan 999`

>Explicit tagging of the native VLAN on all trunk ports. Must be configured on all switches in network autonomy.

`Switch(config)# vlan dot1q tag native`

> Example
As an example of a double tagging attack, consider a secure web server on a VLAN called VLAN2. Hosts on VLAN2 are allowed access to the web server; hosts from outside VLAN2 are blocked by layer 3 filters. An attacking host on a separate VLAN, called VLAN1(Native), creates a specially formed packet to attack the web server. It places a header tagging the packet as belonging to VLAN2 under the header tagging the packet as belonging to VLAN1. When the packet is sent, the switch sees the default VLAN1 header and removes it and forwards the packet. The next switch sees the VLAN2 header and puts the packet in VLAN2. The packet thus arrives at the target server as though it were sent from another host on VLAN2, ignoring any layer 3 filtering that might be in place.