# SNIFFING TOOLS AND METHODS

## TOOLS
Sensors

In-Line

Test Access Point (TAP)

Man-in-the-Middle (MitM)

Out of Band (Passive)

Switched Port Analyzer (SPAN)

## IN-LINE SENSOR
Placed between communicating devices to stop attacks

Intrusion Prevention System (IPS)

Firewall

Impacts network latency

## PASSIVE SENSOR
Monitors network segments

Can detect attacks but cannot stop them

Gets copies of network traffic

Intrusion Detection System (IDS)

Does not impact network latency

## TAP
Appliance placed between 2 network devices

Best for packet collection with no data loss

Must be placed "in line" of network traffic

Not Scalable

Will need several installed to capture traffic for other network segments


## MITM
Attacker can use ARP or some other method/protocol

Attackers can sniff or manipulate traffic that flows through them

Typically must be on the same network as the victim

Traffic capture is dependent on the attacker’s system and bandwidth

## SPAN
Configured on the network Switch

Best for packet collection of traffic from several switch ports at once

Scalable

Can have a high degree of packet loss

Places burden on the network Switch

#  DEFAULT CHARACTERISTICS FOR SYSTEM IDENTIFICATION

## FINGERPRINTING AND HOST IDENTIFICATION
Variances in the RFC implementation for different OS’s and systems enables the capability for fingerprinting

Tools used for fingerprinting and host identification can be used passively(sniffing/fingerprinting) or actively(scanning)

## FINGERPRINTING
### Active OS fingerprinting

Easier

Send packets to the target and monitor response

Tools:

	Nmap

	Xprobe2

	sinfp3

### Passive OS fingerprinting

More difficult

Rely on sniffing packets

Tools:

	p0f

 	p0f -r pcap.pcap

	Ettercap

	PRADS
 
## OPEN PORTS AND PROTOCOLS
Known Windows/Linux ports

Known Windows/Linux protocols

Banner grab service ports

## KNOWN WINDOWS AND LINUX PORTS
Windows

	88 - Kerberos / Domain Controller

	137/138/139 - NetBIOS

	445 - SMB

Linux

	22 - SSH

	111 - SUN RPC

## EPHEMERAL PORTS
IANA 49152–65535

Linux 32768–60999

Windows XP 1025–5000

Win 7/8/10 use IANA

Win Server 2008 1025–60000

Sun Solaris 32768–65535

## PROTOCOL SPECIFIC IDENTIFIERS
HTTP: User-agent strings

https://useragentstring.com/pages/useragentstring.php

SSH: Initial connection

https://goteleport.com/blog/ssh-handshake-explained/

NetBIOS Name Service

https://learn.cnd.ca.gov/Microsoft/NamingConvention/#naming-standards-for-servers


## P0F (PASSIVE OS FINGERPRINTING)
Looks at variations in initial TTL, fragmentation flag, default IP header packet length, window size, and TCP options

Configuration stored in:

	 /etc/p0f/p0f.fp

  
# PERFORM NETWORK TRAFFIC BASELINING

## WHAT IS BASELINING?
Snapshot of what the network looks like during a time frame

No industry standard

7 days to establish the initial snapshot

Prerequisite Information

## NETWORK BASELINE OBJECTIVE
Determines the current state of your network

Ascertain the current utilization of network resources

Identify normal vs peak network traffic time frames

Verify port/protocol usage

## PERFORM BASELINING
Preparation:

Network Diagram

Known Servers, Hosts, and Networking devices

Known IPs, ports, and protocols

Known forbidden IPs, ports, and protocols

Known traffic "flows"

## PERFORM BASELINING
Scope and Objectives:

What traffic/protocols to capture?

Which network segments?

Which days?

What times?

## TRAFFIC FLOW THROUGH PROTOCOL COMMUNICATION ANALYSIS

## USING WIRESHARK
Common Display Filters

Protocol Hierarchy

Conversations

Endpoints

I/O Graph

# NETWORK FORENSICS

## Methodologies

### HACKER METHODOLOGIES
Footprinting

Network scanning

Network Enumeration

Vulnerability Assessment

## CYBER KILL CHAIN

![KILLCHAIN](https://github.com/user-attachments/assets/15a19500-54cf-485f-9d66-193f7ddf23c7)

## MITRE ATT&CK

![attack](https://github.com/user-attachments/assets/fd5ce0d3-4b19-42df-8e3e-6ee7b96de27b)


## MITRE D3FEND

![D3FEND](https://github.com/user-attachments/assets/c0ab6caa-974f-4753-85e0-c640456c4757)

## THE DIAMOND MODEL

![diamond](https://github.com/user-attachments/assets/614fbc4f-b9d5-499c-ad05-4694dedec902)

## NIST CYBER SECURITY FRAMEWORK

![nist](https://github.com/user-attachments/assets/fb1f830a-fc50-4c42-b113-e2425f3f3b12)

# INDICATORS

## ANOMALY DETECTION
### Indicator of Attack (IOA)

Proactive

A series of actions that are suspicious together

Focus on Intent

Looks for what must happen

	Code execution. persistence, lateral movement, etc.


### Indicator of Compromise (IOC)

Reactive

Forensic Evidence

Provides Information that can change

	Malware, IP addresses, exploits, signatures

### SOME INDICATORS
.exe/executable files

NOP sled

Repeated Letters

Well Known Signatures

Mismatched Protocols

Unusual traffic

Large amounts of traffic/ unusual times

## SIGNS OF IOA
Destination IP/Ports

Public Servers/DMZs

Off-Hours

Network Scans

Alarm Events

Malware Reinfection

Remote logins

High amounts of some protocols

## SIGNS OF IOC
Unusual traffic outbound

Anomalous user login or account use

Size of responses for HTML

High number of requests for the same files

Using non-standard ports/ application-port mismatch

Writing changes to the registry/system files

Unexpected/unusual patching or tasks

# TYPES OF MALWARE

## ADWARE/SPYWARE
large amounts of traffic/ unusual traffic

IOA

	Destinations

IOC

	Unusual traffic outbound

##  VIRUS
phishing/ watering hole

IOA

	Alarm Events, Email protocols

IOC

	Changes to the registry/ system files

 ## WORM

 phishing/ watering hole

IOA

	Alarm events

IOC

	changes to registry/ system files

 ## TROJAN
beaconing

IOA

	Destinations

IOC

	Unusual traffic outbound, unusual tasks, changes to registry/ system files

## ROOTKIT
IOA

	Malware reinfection

IOC

	Anomalous user login/ account use


## BACKDOOR
IOA

	Remote logins

IOC

	Anomalous user login/ account use

##  BOTNETS
large amounts of IPs, C2 server traffic

IOA

	Destinations, remote logins

IOC

	Unusual tasks, anomalous user login/ account use

## POLYMORPHIC/METAMORPHIC MALWARE
Depends on the malware type/class

## RANSOMWARE
IOA

	Destinations, Ports, Malware reinfection

IOC

	Unusual traffic outbound, non-standard ports, unusual tasks

 ## MOBILE CODE
IOA

	Depends on the malware type/class

 
## BIOS/FIRMWARE MALWARE
IOA

	Malware reinfection

IOC

	Depends on the malware type/class


 # NETWORK ANOMALIES THROUGH TRAFFIC ANALYSIS

 ## ICMP TUNNELING

 ![icmp-tunnel](https://github.com/user-attachments/assets/7fe68cce-e65b-4439-9d44-e4770d010cf9)

ICMP PING uses Type 8 and Type 0

Both should be:

	1 for 1

	Same size and payload

Look out for:

	Request/Reply imbalances

	Abnormal/different payloads

## DNS TUNNELING
<img width="992" alt="dns-tunnel" src="https://github.com/user-attachments/assets/2832163c-ba26-40f6-8b70-8103ce286765">

DNS uses Query/Response

	1 Query typically gets 1 response

Look out for:

	Query/Response imbalances

	Abnormal/different payloads

	Continuous Queries

## HTTP(S) TUNNELING
HTTP is "bursty" in nature

Client issues request and the server responds

Look out for:

	Steady connections

	HTTPs you will need to check session establishment for abnormalities

##  BEACONING
![beacons](https://github.com/user-attachments/assets/bdec014b-9bfc-42be-881a-e1256ec842db)

Call back to the C&C server

Gets/sends commands from/to C&C

Look out for:

	Beacon Timing

		Commonly at regular intervals

Beacon Size

	Check-Ins may not have any payloads

	Orders will have payloads


 








 
