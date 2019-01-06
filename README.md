OpenVPN
=======

# Introduction

OpenVPN establishes a Virtual Private Network to secure communication over an untrusted supporting network. It implements a custom protocol on-top of the transport network layer to encrypt the traffic point-to-point, different from IPsec, and uses the cryptographic protocol **TLS** for key exchange to ensure the integrity and confidentiality of the communication via the **OpenSSL** encryption library. Members off the VPN authenticate each other using pre-shared cryptographic certificates or alternatively shared credentials (*username* and *password*). Latter case won’t be further considered in this document.
In a typical setup there’s one node functioning as the role of a VPN server providing access to a secure resource and enables nodes functioning as the role of clients, usually remote to the servers network via the WAN/Internet, to connect to and access the resource. Depending on the servers configuration the clients me or may not be able to see or communicate with each other. This server has its own server certificate which all clients need a copy of to authenticate the server and each client has its own client certificate which need to be kept secret.
jjgg
# Motivation
## Untrusted networks
In _public_ networks like open hotspots which provide free Internet to costumers the medium over which network traffic is send can't be trusted with **integrity** and **confidentiality** **of** your information.
Because
- Wireless networks are open to listening
- Network services can be hijacked
- Man-in-the-Middle attacks are easy

For this reason a virtual private network can be used to _upgrade_ your public network to a trusted network to send traffic in encrypted form over.

## Securing access to resources

# Trust
## CA or PKI
The client needs to be able to trust the remote VPN server is who he says he it is to establish an SSL/TLS connection

# Encryption
## Public Key Cryptography via certificates

## Handshake
OpenSSL implements hybrid encryption. Asymmetric encryption via pre-shared certificates containing the public key and symmetric encryption during a session for all _real_ traffic for a combination of security and performance (throughput).


# Controls in ISO 27002
## A.13.2.1: Information transfer policies and procedures
With:
- Procedures to protect the data from manipulation, destroying...
- Using cryptographic techniques **(AES)**

## A.10.1.2: Key management
With:
- Generation of the keys **(Diffie-Hellman-KeyExchange)**
- Distribution of keys including the usage

## A.10 Cryptography in general

# Source
https://www.lynda.com/SSL-tutorials/Trust-encryption-network/178124/196828-4.html