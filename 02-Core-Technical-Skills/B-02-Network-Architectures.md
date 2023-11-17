# Network Architectures

## Cat 5 / Fibre

- Ref: https://en.wikipedia.org/wiki/Category_5_cable
- Ref: https://www.techjunkie.com/ethernet-vs-fiber-optic-cables/#:~:text=While%20this%20is%20lightning%20fast,four%20pairs%20inside%20the%20cable.

## 10/100/1000baseT
- Ref: https://en.wikipedia.org/wiki/Gigabit_Ethernet

### 100BASE-T (Fast Ethernet)
Can be any of the Fast Etherenet `802.3` standards for twisted pair cable, but is typically `802.3u-1995` **(100BASE-TX)** for most installations. Fast Etherenet has a speed of 100 Mbit/s and a max distance of 100 metres.

- The wiring for 100BASE-TX uses Cat-5 cable, with 8 pins made up of 4 pairs. 
- Each pair is used for one direction (`send` or `receive`), allowing full-duplex operation. 
- Specifically, pins 1 and 2 are one pair, with pins 3 and 6 being the other pair. For 10/100BASE-T, only two pairs are required to send and transmit.
- A pair makes an electrical circuit which allows `1s` and `0s` (encoded) to be trasmitted from one node, and received back. The opposite pair would be used for the remote node to transmit and receive back.

### 1000BASE-T (Gigabit Ethernet)

- IEEE 802.3ab standard.
- Can use Cat-5 cabling or Fibre optic. 
- When using Cat-5 cables, it requires 4 pin pairs to transmit and receive data.
- Can reach speeds of 1000 Mbit/s.
- When using Cat-5 copper cabling, max distance is still 100 metres. When using Fibre, max distance can be 5 km on 1000BASE-LX.

## Token ring
- Ref: https://en.wikipedia.org/wiki/Token_Ring

## Wireless (802.11)

IEEE 802.11 is the local area network standard for wireless networks. Wireless networking operates using radio waves within a fixed size spectrum. The radio spectrum is regulated by government, who allocates bands for general electronic emissions (ISM), ranging from:
- mircrowaves
- cordless phones
- bluetooth
- garage door openers

The band of wireless spectrum allocated to 802.11 is:
- 2.4-GHz
- 5-GHz

Wireless adapters and access points can support different 802.11 standards, which in turn support either the 2.4-GHz or 5-GHz frequencies. If the support the they are dual-band devices. A list of the wireless standards, supported frequencies and Wi-Fi Alliance names are shown below:

|IEEE Standard|802.11a|802.11b|802.11g|802.11n|802.11ac|802.11ax|802.11be|
|-------------|-------|-------|-------|-------|--------|--------|--------|
|Wi-Fi Alliance Name|Wi-Fi1|Wi-Fi2|Wi-Fi3|Wi-Fi4|Wi-Fi5|Wi-Fi6/6E|Wi-Fi7|
|Year Released|1999|1999|2003|2009|2014|2019|2024/2025|
|Frequency|5GHz|2.4GHz|2.4GHz|2.4GHz, 5GHz|2.4GHz, 5GHz|6: 2.4GHz, 5GHz / 6E: 2.4GHz|2.4GHz, 5HGz, 6GHz|
|Maximum Data Rate|54Mbps|11Mbps|54Mbps|600Mbps|1.3Gbps|10-12Gbps|40Gbps|

To maximise the allocated spectrum, Wi-Fi is split up into channels, with each section having their own portion of the frequency range. 
- Channels within the 2.4-GHz range are numbered 1-14.
- Channels with the 5-GHz range are non-consecutively numbered 36-165.
- Channels are labeled the same globally, but some contries place restrictions on particular channnels.
- When one Access Point (AP) is in use, the AP and clients transmit on one preconfigured channel. If one device is transmitting on channel 1 and another transmits on channel 2 at the same time, the two will clash due to electromagnetic inteference because the channels overlap in frequency range.

On 2.4GHz frequencies, the channels known not to overlap are **1**, **6**, **11** and **14**

### Sessions

To communicate on a Wi-Fi network:
1. A client must establish a connection with the AP by sending a broadcast message *(prob request)* to the Service Set Identifier `SSID`. A probe request asks the network  to identify itself.
2. It sends probe requests on all the channels until the AP responds with a *Probe Response* or the time it expects a response by expires.
3. Next, the client sends and *authentication request*. This is unrelated to other security authentication requests like WPA.
4. If the AP is configured to accept any connection *(Open)*, the connection succeeds and the client sends an *association request*. If it is configured to use security, then the client must supply a shared-key.
5. Once the AP responds with an *association response*, the client is tracked by the AP and can communicate on the network if there are no further security requirements.

## Security implications of shared media, switched media and VLANs

### Shared Media

Ethernet was originally based on the idea of computers communicating over a shared coaxial cable acting as a broadcast transmission medium. Ethernet's shared coaxial cable (the shared medium) traversed a building to every attached machine. The carrier-sense multiple access with collision detection (CSMA/CD) scheme was used by computers to communicate on this shared the channel. 

The security implications with using shared media for communications is:
- Any information sent by one computer is received by all.
- Collisions happen if two machines transmit at the same time. This could intentially be done to cause a DoS on the network.

### Switched Media

### VLANs

- Copy paste from Wikapedia
- Ref: 

**VLAN hopping:** is an OSI layer 2 based network attack on virtual LAN (VLAN) devices operating using VLAN tagging. The basic concept behind all VLAN hopping attacks is for an attacking host on a VLAN to gain access to traffic on other VLANs that would normally not be accessible. There are two primary methods of VLAN hopping: 
- switch spoofing
- double tagging. 

Both attack vectors can be mitigated with proper switch port configuration.

**Switch spoofing:**
An attacking host imitates a trunking switch by speaking the tagging and trunking protocols (e.g. **IEEE 802.1Q**, **Dynamic Trunking Protocol**) used in maintaining a VLAN. Traffic for multiple VLANs is then accessible to the attacking host.

> **Switch spoofing mitigation:**
Switch spoofing can only be exploited when interfaces are set to negotiate a trunk. To prevent this attack on Cisco IOS, use one of the following methods 

> 1. Ensure that ports are not set to negotiate trunks automatically by disabling DTP:

`Switch (config-if)# switchport nonegotiate`

> 2. Ensure that ports that are not meant to be trunks are explicitly configured as access ports

`Switch (config-if)# switchport mode access`

**Double tagging:**
- *An attacker connected to an 802.1Q-enabled port prepends **two VLAN tags** to a frame that it transmits*. 
- The frame *(externally tagged with VLAN ID that the attacker's port is really a member of*) is forwarded without the first tag because it is the native VLAN of a trunk interface. 
- The second tag is then visible to the second switch that the frame encounters. This second VLAN tag indicates that the frame is destined for a target host on a second switch. 
- The frame is then sent to the target host as though it originated on the target VLAN, effectively bypassing the network mechanisms that logically isolate VLANs from one another. However, possible replies are not forwarded to the attacking host (unidirectional flow).

**Double tagging mitigation:**
- Double Tagging can only be exploited on switch ports configured to use native VLANs.  Trunk ports configured with a native VLAN don't apply a VLAN tag when sending these frames. This allows an attacker's fake VLAN tag to be read by the next switch.

- Double Tagging can be mitigated by any of the following actions (Incl. IOS example):

1. Simply do not put any hosts on VLAN 1 (The default VLAN). i.e., assign an access VLAN other than VLAN 1 to every access port:
 
 `Switch (config-if)# switchport access vlan 2`

2. Change the native VLAN on all trunk ports to an unused VLAN ID.

`Switch (config-if)# switchport trunk native vlan 999`

3. Explicit tagging of the native VLAN on all trunk ports. Must be configured on all switches in network autonomy.

`Switch(config)# vlan dot1q tag native`

**Example:**

As an example of a double tagging attack, consider a secure web server on a VLAN called VLAN2. 

- Hosts on VLAN2 are allowed access to the web server; hosts from outside VLAN2 are blocked by layer 3 filters. 

- An attacking host on a separate VLAN, called VLAN1(Native), creates a specially formed packet to attack the web server. It places a header tagging the packet as belonging to VLAN2 under the header tagging the packet as belonging to VLAN1. 

- When the packet is sent, the switch sees the default VLAN1 header and removes it and forwards the packet. 

- The next switch sees the VLAN2 header and puts the packet in VLAN2. 
- The packet thus arrives at the target server as though it were sent from another host on VLAN2, ignoring any layer 3 filtering that might be in place.