OpenVPN
=======

- [OpenVPN](#openvpn)
- [Introduction](#introduction)
- [Motivation](#motivation)
  - [Information Security in Untrusted networks](#information-security-in-untrusted-networks)
  - [Securing access to restricted resources](#securing-access-to-restricted-resources)
- [Alternatives](#alternatives)
- [Trust](#trust)
  - [Public Key Infrastructure (PKI)](#public-key-infrastructure-pki)
  - [Certificate Authority (CA)](#certificate-authority-ca)
- [Encryption](#encryption)
  - [Authentication](#authentication)
    - [Password based login authentication](#password-based-login-authentication)
    - [Static key](#static-key)
    - [Public Key Cryptography via certificates](#public-key-cryptography-via-certificates)
    - [Login via authentication server (LDAP)](#login-via-authentication-server-ldap)
  - [Handshake](#handshake)
  - [Traffic encryption](#traffic-encryption)
- [Security Controls in ISO 27k documents](#security-controls-in-iso-27k-documents)
  - [A10 Cryptography controls in 27K:](#a10-cryptography-controls-in-27k)
    - [10.1.1 Policy on the use of cryptographic controls](#1011-policy-on-the-use-of-cryptographic-controls)
    - [A.10.1.2: Key management](#a1012-key-management)
- [Source](#source)

# Introduction

OpenVPN establishes a Virtual Private Network to secure communication over an untrusted supporting network. It implements a custom protocol on-top of the transport network layer to encrypt the traffic point-to-point, different from IPsec, and uses the cryptographic protocol **TLS** for key exchange to ensure the integrity and confidentiality of the communication via the **OpenSSL** encryption library. Members off the VPN authenticate each other using pre-shared cryptographic certificates or alternatively shared credentials (*username* and *password*). Latter case won’t be further considered in this document.
In a typical setup there’s one node functioning as the role of a VPN server providing access to a secure resource and enables nodes functioning as the role of clients, usually remote to the servers network via the WAN/Internet, to connect to and access the resource. Depending on the servers configuration the clients me or may not be able to see or communicate with each other. This server has its own server certificate which all clients need a copy of to authenticate the server and each client has its own client certificate which need to be kept secret.

# Motivation
## Information Security in Untrusted networks
In _public_ networks like open hotspots which provide free Internet to costumers the medium over which network traffic is send can't be trusted with **integrity** and **confidentiality** of your information.
Because
- Wireless networks are open to listening
- Network services can be hijacked
- Man-in-the-Middle attacks are easy

For this reason a virtual private network can be used to _upgrade_ your public network to a trusted network to send traffic in encrypted form over.

## Securing access to restricted resources

A Virtual Private Network is established to allow the client access to restricted resources through a private _VPN tunnel_, securing the information send from and to the resource no matter the carrier network.

# Alternatives
There exist a several VPN alternatives but mostly closed-source or proprietary. For some use-cases SSH may be used for the tunneling feature.

# Trust
The client needs to be able to trust the remote VPN server is who he says he it is to establish an SSL/TLS connection.

## Public Key Infrastructure (PKI)
For this reason PKI is used. PKI uses a public/private key pair to manage a secured communication which involves issuing and revoking certificates,creating and publishing CRLs,storing and retrieving certificates and CRLs and key life cycle management.Encryption yields confidentiality while digital signatures yields Integrity.
PKI manages the keys and digital used to implement Cryptography within applications such as email and messaging,web browser and web servers ,Electronic data interchange; in applications that establish secure network transactions or communication sessions
Over the web or in VPN using protocols such as S/MIME,SSL and IPSEC; and in functions such as digitally signed documents or code In addition,application developed in-house can be PKI-enabled.

## Certificate Authority (CA)
A Certified Authority is a body that issues certificates to persons or organizations. The CA signs the certificate thereby authenticating the identity of the requestor. In,Addition,the CA stamps the certificate with an expiration date.The CA may return the certificate to the requesting system and /or post it in a repository.

# Encryption
## Authentication
OpenVPN supports multiple authentication methods allowing the client to proof to the server _he says who he is_

### Password based login authentication
The client authenticates using using a user and password combination to send to the VPN Server. No advanced security like trust established.

**Attack**
Insecure sharing of key

### Static key
A pre-shared static key for point-to-point encryption is used. The VPN Server knows of the possible clients and if the key is compromised, all traffic including past recorded traffic can be decrypted.

**Attack**
Theft of media containing key, Insecure sharing of key

### Public Key Cryptography via certificates
A perfect forward security is established using pre-shared certificates signed by a commonly trusted CA.
The VPN Server doesn't need to have or know of all the client certificates which may connect to it.
If the current session key is compromised due to an attack only the current session can be decrypted, not past sessions which may have been recorded

**Attack**
DMA devices, Cold-boot attack, kernel exploit

### Login via authentication server (LDAP)

## Handshake
OpenSSL implements hybrid encryption. Asymmetric encryption via pre-shared certificates containing the public key and symmetric encryption during a session for all _real_ traffic for a combination of security and performance (throughput).

## Traffic encryption

# Security Controls in ISO 27k documents
From ISO 27002 Appendix

A 9 Business requirements of access control
To limit access to information and information processing facilities

**13.2.1: Information transfer policies and procedures**
Objective: To maintain the security of information transferred within an organization and with any external entity

**9.1.2 Access to networks and network services**

## A10 Cryptography controls in 27K:
Effectively use cryptographic tools

### 10.1.1 Policy on the use of cryptographic controls

### A.10.1.2: Key management
With:
- Generation of the keys **(Diffie-Hellman-KeyExchange)**
- Distribution of keys including the usage

# Source
https://www.lynda.com/SSL-tutorials/Trust-encryption-network/178124/196828-4.html
https://www.cisco.com/c/en/us/products/security/vpn-endpoint-security-clients/what-is-vpn.html