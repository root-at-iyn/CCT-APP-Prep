# Applications of Cryptography

## SSL

## IPSec

IPSec is a suite of protocols used to secure internet connections. The protocols involved are: 
- **Authentication Header (AH) - (Protocol 51)**: Used to provide data integrity, anti-replay and authentication. It is not suitable for sending secret information as AH alone does not provide encryption.
- **Ecapsulating Security Payload (ESP) - (Protocol 50)**: Used to provide authentication, data integrity, and confidentiality. Confidentiality is achieved by encapsulating the entire original IP packet when using tunnel mode. A new packet header is added and the inner (encapsualted) packet is encrypted, however the new outer packet header is remains unprotected.
- **Internet Key Exchange (IKE) (UDP 500)**: Used to setup a secure authenticated communication channel between two peers. IKE uses either a Pre-Shared Key (PSK) or X.509 PKI certificates for authentication, and the Diffie-Hellman key exchange (DH) protocol to setup a shared session secret.

Ref:
- https://en.wikipedia.org/wiki/IPsec#Security_association
- https://en.wikipedia.org/wiki/Internet_Key_Exchange


## SSH

## PGP

## Common wireless (802.11) encryption protocols:
### - WEP
### - WPA
### - TKIP
