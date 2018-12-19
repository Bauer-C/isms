OpenVPN
=======

# Introduction

OpenVPN establishes a Virtual Private Network to secure communication over an untrusted supporting network. It implements a custom protocol on-top of the transport network layer to encrypt the traffic point-to-point, different from IPsec, and uses the cryptographic protocol **TLS** for key exchange to ensure the integrity and confidentiality of the communication via the **OpenSSL** encryption library. Members off the VPN authenticate each other using pre-shared cryptographic certificates or alternatively shared credentials (*username* and *password*). Latter case won’t be further considered in this document.
In a typical setup there’s one node functioning as the role of a VPN server providing access to a secure resource and enables nodes functioning as the role of clients, usually remote to the servers network via the WAN/Internet, to connect to and access the resource. Depending on the servers configuration the clients me or may not be able to see or communicate with each other. This server has its own server certificate which all clients need a copy of to authenticate the server and each client has its own client certificate which need to be kept secret.

# Motivation
- Public hotspots (open wireless networks) are open to listening therefore traffic can be intercepted and/or modified
- Network services can be hijacked or replaced
- Man-in-the-middle (MitM) attacks are easy
- Securing the network properly is _hard_, vulnerabilities get discovered often

# Trust
- SSL proves via signed certificates the server is who he claims to be

# Sources
https://www.lynda.com/SSL-tutorials/Trust-encryption-network/178124/196828-4.html