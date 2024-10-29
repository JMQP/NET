# Layer 5


## Virtual Private Networks

Types:

  Remote Access(client-to-site)

  Site-to-Site

## L2TP (UDP 1701)

![image](https://github.com/user-attachments/assets/a925c42d-1f1f-475d-85cf-82c64036dde3)

RFC 2661

Origins from Cisco L2F and Microsoft PPTP

Tunnel only. No Encryption

## PPTP (TCP 1723)


![pptp](https://github.com/user-attachments/assets/d49d3add-ec33-4993-9615-4940e36fc134)

RFC 2637

Microsoft

Provides encryption

Obsolete with many vulnerabilities

# L2F (UDP 1701)

![l2tp](https://github.com/user-attachments/assets/ee46a5dd-e12f-461a-bd87-493cafe01625)

Cisco

Tunnel only. No Encryption

Requires L2F Network Server (LNS) and a L2F Access Concentrator (LAC)

## IPSEC
Modes: Transport or Tunnel

Headers:

	ESP (protocol 50)

	AH (protocol 51)

	IKE (UDP port 500 or 4500)

## IPSEC - TRANSPORT

![ipsectrans](https://github.com/user-attachments/assets/cb1771e7-4826-4e93-8391-b9b2e42fbe71)

## IPSEC - TUNNEL

![ipsectunnel](https://github.com/user-attachments/assets/147fe465-3f5e-48fe-9428-61000f3f3bce)

## OPENVPN
Open source

Uses OpenSSL for encryption

UDP*/TCP port 1194

# Proxies


![basic_proxy](https://github.com/user-attachments/assets/17a9f992-a2c4-4483-b8bd-94402476cd77)

## SOCKS 4/5 (TCP 1080)

RFC 1928

Uses various Client / Server exchange messages

Client can provide authentication to server

Client can request connections from server

## SOCKS4
No Authentication

Only IPv4

No UDP support

No Proxy binding. Client’s IP is not relayed to destination.

 ## SOCKS5
Various methods of Authentication

IPv4 and IPv6 support

UDP support

Supports Proxy binding. Client’s IP is relayed to destination.

## NETWORK BASIC INPUT OUTPUT SYSTEM (NETBIOS) PROTOCOL
TCP 139 and UDP 137/138

Name Resolution (15 characters)

Largely replaced by DNS

## SMB/CIFS (TCP 445)
￼
![smb](https://github.com/user-attachments/assets/f1048ba3-303e-45ad-afcd-f819e0642363)


SMB Rides over Netbios

	Netbios Dgram Service - UDP 138

	Netbios Session Service - TCP 139

	SAMBA and CIFS are just flavors of SMB

## RPC (ANY PORT)
Allows a program to execute a request on a local/remote computer

Hides network complexities

XML, JSON, SOAP, and gRPC

User application will:

	Request for information from external server

	Receives the information from the external server

	Display collected data to User

#  API
Framework of rules and protocols for software components to interact.

Methods, parameters, and data formats for requests and responses.

REST and SOAP


# Layer 6

## RESPONSIBILITIES
Translation

Formating (Turning data into something we can use

Encoding (ASCII, EBCDIC, HEX, BASE64)

Encryption (Symmetric or Asymmetric)

Compression

# Layer 7

## Protocols and Headers

## TELNET (TCP 23)

![telnet](https://github.com/user-attachments/assets/7d223613-4cef-4c82-80ba-5b93d449b76f)

Remote Login

Authentication

Clear Text

Credentials susceptible to interception

## SSH (TCP 22)

![ssh](https://github.com/user-attachments/assets/0faefcc8-4d95-48c8-8e57-f278b4953f60)

Messages provide:

	Client/server authentication

	Asymmetric or PKI for key exchange

	Symmetric for session

	User authentication

	Data stream channeling

## COMPONENTS OF SSH ARCHITECTURE
Client / Server / Session

Keys

	User Key - Asymmetric public key used to identify the user to the server

	Host Key - Asymmetric public key used to identify the server to the user

	Session Key - Symmetric key created by the client and server to protect the session’s

## SSH ARCHITECTURE

![ssh_architecture](https://github.com/user-attachments/assets/b0fca04c-45c0-4b52-8cf0-5921c2bd8dba)

ssh is the protocol

sshd is the ssh daemon

![ssh_protocol](https://github.com/user-attachments/assets/be2fddcd-8135-4f30-859c-8d98be3846f0)


## SSH IMPLEMENTATION CONCERNS
Using password authentication only

Key rotation

Key management

Implementation specification (libssh, sshtrangerthings)

libssh exploits sshv2

## SSH Usage

ssh user@ip.ip.ip.ip

### SSH Options

-p {port} - Alternate port
-l {username} - Specify the username
-X - Enable X11 forwarding
-v(vv) - Add logging and debugging
-i {identity file} - Specify a private key identity
-F {config file} - Specify an alternate user config file
-N - Do not send remote commands
-T - Do not create a pseudo vty
-C - Enable compression
-f - Backgroud process after authentication
-J user@host - Proxy jump
-L [bind_address:]port:host:hostport
-R [bind_address:]port:host:hostport
-D {port}

## SSH First Connect

You will ned to approve server host (public)

Key is saved to 

	/home/student/.ssh/known_hosts

 ## SSH Reconnect

 Further SSH connections to server will not prompt to save key as long as key does not change
	



