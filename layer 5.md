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
	

## SSH Key Change Fix 

	ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"
 
Copy/Paste the ssh-keygen message to remove the Host key from the known_hosts file

When you re-connect it will prompt you to save the new Host key

## SSH Files

Known-Hosts Database

	~/.ssh/known_hosts

Configuration Files

	/etc/ssh/ssh_config
	/etc/ssh/sshd_config


## VIEW/CHANGE SSH PORT
To view the current configured SSH port

	cat /etc/ssh/sshd_config | grep Port
Edit file to change the SSH Port

	sudo nano /etc/ssh/sshd_config
Restart the SSH Service

	systemctl restart ssh

 SSH-KeyGen

 	ssh-keygen -t rsa -b 4096 -C "Student"
  
Create your own SSH Public/Private keys

	-t Encryption (rsa|dsa|ecdsa|ed25519)

	-b Bit length (1024|2048|4096)

	-C Adds a comment

~/.ssh/id_rsa and ~/.ssh/id_rsa.pub

## SSH-COPY-ID
	ssh-copy-id student@172.16.82.106
Copies your SSH Public key to the remote server

Saves key to ~/.ssh/authorized_keys on remote server

Allows you to authenticate with server using your key instead of password

Must secure your private key
  
## HTTP(S) (TCP 80/443)

![http](https://github.com/user-attachments/assets/d495e297-3d0d-4517-bd47-343a2c68ec9e)

User Request methods(HTTP)

	GET / HEAD / POST / PUT

Server response Codes(HTTP)

	100, 200, 300, 400, 500

##  HTTP(S) VULNERABILITIES
Flooding

Amplification

Low and slow

Drive-By Downloads

BeEF Framework

## DNS (TCP(Zone Transfer/UDP (Queries) 53) 
![dns](https://github.com/user-attachments/assets/85a1e894-f6e4-4071-842a-23bd795ff276)

## DNS QUERY/RESPONSE
Resolves Names to IP addresses

Queries and responses use UDP

DNS response larger than 512 bytes use TCP

	DNS Zone Transfer

	DNS Security

 ## DNS Records

 A - IPv4 record

AAAA - IPv6 record

MX - Mail Server record

TXT - Human-readable text

NS - Name Server record

SOA - Start of Authority


## DNS Architecture
![DNS_Architecture](https://github.com/user-attachments/assets/6fe6db73-a361-4984-a439-13ab61307c80)


## FTP (TCP 20/21)
![ftp](https://github.com/user-attachments/assets/132bf30e-3c9a-4bd6-a6c3-8e6b0b578e46)

	RFC 959

	Port 21 open for Control (In WS: GET,POST)

	Port 20 only open during data transfer(In WS: data)

Authentication or Anonymous

Clear Text

Modes:

	Active (default)

	Passive

## FTP Active

![ftp_active](https://github.com/user-attachments/assets/23d86990-5378-47f6-8e31-408b21c25384)


## FTP ACTIVE ISSUES

NAT and firewall traversal issues

Complications w/tunnel through ssh

Passive FTP solves issues related with Active mode and is most often used in modern systems


## FTP Passive


![ftp_passive](https://github.com/user-attachments/assets/15066f00-334c-4e13-a140-a1f65f10064c)

# TFTP (UDP 69)

![tftp](https://github.com/user-attachments/assets/73ec3aed-ba13-4503-99e0-ea9038347b18)

clear text

Reliably provided at App layer

Used by routers and switched to transfer IOS and config files


# SMTP (TCP 25)
![smtp](https://github.com/user-attachments/assets/99edbca1-fc91-4d9f-a98a-9a959a9a2a02)

used to send mail 

no encrpytion

smtp over TLS/SLL (SMTPS)
	TCP Ports 587 and 465

# POP (TCP 110)

receives mail

no sync with server 
 
no enc

POP3

# IMAP (TCP 143)
receives email

sync with server

no enc

IMAP4
# DHCP (UDP 67/68)
![dhcp](https://github.com/user-attachments/assets/f7a200bf-841f-4506-9ccd-cad2d8d2b3e8)

## DHCPV4
Dora

	Discover(Broadcast)
 	Offer(Unicast)
  	Request(Broadcast)
   	Acknowlegde (Unicast)
## DHCPV6

if managed flag is set suring SLAAC:

	Solicit (Multi)
 	Advertise(Unicast)
  	Req or Info req (Multi)
   	Reply (Uni)

# DHCP VUL
Rogue DHCP

Evil Twin

DHCP Starvation

# NTP (UDP 123)

Stratum 0 - authoritative time source

Up to Stratum 15

Vulnerable to crafted packet injection
    

## AAA PROTOCOLS
Authentication, Authorization, and Accounting

For third party authentication

# TACACS (TCP 49) SIMPLE/XTENDED
![tacacs-s](https://github.com/user-attachments/assets/1058bd7d-fddf-41b0-9303-deee256b372d)


![tacacs-e](https://github.com/user-attachments/assets/6f95d580-9ba0-480a-8137-47ada7df5c28)

# RADIUS (UDP 1645/1646 AND 1812/1813)
![radius](https://github.com/user-attachments/assets/d0e7a650-41f4-42b2-8b93-02c476efdacd)

# DIAMETER (TCP 3868)

![Diameter_Header](https://github.com/user-attachments/assets/63d16670-a963-402e-890b-b4defd846ea2)


snmp (udp 161/162)

![snmp](https://github.com/user-attachments/assets/ccf13e28-f8f4-458d-a352-96bc63fad9d0)


Versions:

	SNMPv1 - RFC 1157

	SNMPv2c - RFC 1441

	SNMPv3 - RFC 3410

7 Message Types

	Get Request

	Set Request

	Get Next

	Get Bulk

	Response

	Trap

	Inform


#  SNMP VULNERABILITIES
v1 and 2c

Weak Community Strings

Lack of Encryption

Information Disclosure

Can be "sniffed"


# RTP (UDP ANY ABOVE 1023)
![rtp](https://github.com/user-attachments/assets/767e48ce-f0e5-45c2-8ebd-5d4fcb0bb7fa)

# RDP (TCP 3389)

Developed by Microsoft (Open Standard)

	No server software needed

Other Proprietary RDP software

	Requires to have 3rd pary software installed

# KERBEROS (UDP 88)
Secure network authentication protocol

Clients obtain tickets to access services

Mutual authentication

Used by Active Directory

# LDAP(S) (TCP 389 AND 636)
Client/server model

Hierarchical

Directory schema

Unsecure and secure versions





