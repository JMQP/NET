# SECURE SHELL (SSH)

Various Implementations (v1 and v2)

Provides authentication, encryption, and integrity.

Allows remote terminal sessions

Can enable X11 Forwarding

Used for tunneling and port forwarding

Proxy connections (Proxy change thing we were talking about yesterday)

CAN TUNNEL OTHER PROTOCOLS THROUGH SSH


## SSH ARCHITECTURE
Client vs Server vs Session

Keys:

	User Key - Asymmetric public key used to identify the user to the server

	Host Key - Asymmetric public key used to identify the server to the user

	Session Key - Symmetric key created by the client and server to protect the session’s communication.

 ## CONFIGURATION FILES
Client Configuration File (/etc/ssh/ssh_config)

Server Configuration File (/etc/ssh/sshd_config)

Known Hosts File (~/.ssh/known_hosts)

## SSH COMPONENTS
![ssh_architecture](https://github.com/user-attachments/assets/189eb062-c3f5-457f-8e08-d38015151c7a)

## SSH ARCHITECTURE

![ssh_protocol](https://github.com/user-attachments/assets/fcb0b841-43fa-4041-b754-85394e2f6c7b)

## SSH FIRST CONNECT
```
student@internet-host:~$ ssh student@172.16.82.106
The authenticity of host '172.16.82.106 (172.16.82.106)' can't be established.
ECDSA key fingerprint is SHA256:749QJCG1sf9zJWUm1LWdMWO8UACUU7UVgGJIoTT8ig0.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '172.16.82.106' (ECDSA) to the list of known hosts.
student@172.16.82.106's password:
student@blue-host-1:~$
```

You will need to approve the Server Host (Public) Key

Key is saved to /home/student/.ssh/known_hosts

## SSH RE-CONNECT
```
ssh student@172.16.82.106
student@172.16.82.106's password:
student@blue-host-1:~$
```

Further SSH connections to server will not prompt to save key as long as key does not change

## SSH HOST KEY CHANGED

```
ssh student@172.16.82.106
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:RO05vd7h1qmMmBum2IPgR8laxrkKmgPxuXPzMpfviNQ.
Please contact your system administrator.
Add correct host key in /home/student/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /home/student/.ssh/known_hosts:1
remove with:
ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"
ECDSA host key for 172.16.82.106 has changed and you have requested strict checking.
Host key verification failed.
```

## SSH KEY CHANGE FIX

```
ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"
```

Copy/Paste the ssh-geygen message to remove the Host key from the known_hosts file


# SSH PORT FORWARDING
Creates channels using SSH-CONN protocol

Allows for tunneling of other services through SSH

Provides insecure services encryption

## SSH OPTIONS
-L - Creates a port on the client mapped to a ip:port via the server (only on internet host, in this course)

-D - Creates a port on the client and sets up a SOCKS4 proxy tunnel where the target ip:port is specified dynamically

-R - Creates the port on the server mapped to a ip:port via the client

-NT - Do not execute a remote command and disable pseudo-tty (will hang window)

# LOCAL PORT FORWARDING

	ssh -p <optional alt port> <user>@<server ip> -L <local bind port>:<tgt ip>:<tgt port> -NT

or

	ssh -L <local bind port>:<tgt ip>:<tgt port> -p <alt port> <user>@<server 

 e.g.

 	ssh <user>@<ip> -L <bind_port>:<tgt_IP>:<tgt_port>

### IN CLASS ex
Ports available Net5

5XXYY

X's = Student #

Y's = 00-99

Map Host to see vul ports

	IH> nmap BH1 -T4 -vvvv -p21-23,80
 
You find ports 21, 22, 23, 80 are open
  
Make sure port 22 uses ssh

	nc BH1 22

 	Open SSh

Now that it's confirmed run ssh 

	IH>ssh user@BH1 - L 52200:127.0.0.1:80 -NT
 
 (use a port in your range, then to the loopback net on port 80 so you can use FTP and other http services)
 
 Next you need to map your port forward

 	nc 127.0.0.1 52200

  Hit "Enter" key twice

  Type in gibberish to confirm, if <html> format returns, your connection is successful

  Now that you have established connection, utilize "wget" to interact with files

  	IH>wget 127.0.0.1:52200 -r 

   This will create a directory and an "index" file in that directory

   To read it 

   	cat 127.0.0.1:52200/index.html

### SSH to BH1

	ssh user@BH1

 First Steps

 	ip a #will tell you all the interfaces ips
  
  	hostname # gives actual hostname
   
   	whoami 

    	ip n #tells you what hosts in the net that this host has talked to recently

     	uname -a # kernel version of system

      	ip r #will tell us about other networks the host knows 

       cat /etc/passwd #more useful for sec

       netstat or ss -ntlp #show tcp ports and ip addresses

ping sweep on box that is on the network that you are not


       	for i in {1..254} ;do (ping -c 192.168.1$i | grep "bytes from" ; done
	
 
Proxy chain

 	IH> ssh@BH1 -D 9050 -NT

  0.0.0.0 on unix netstat readout means any ip on that sytem

  	IH>proxychains nmap -T4 -vvvv -p 21-23,80 192.168.1.10 -Pn

When you use proxy chains you are using whatever host you are authenticating to 

	proxychains nc 127.0.0.1 21

 proxy chains allows you to send any TCP traffic to any host on other side of tunnel

 	proxychians wget -r ftp://127.0.0.1

  	ftp>passive

   DRAGONS ON OTHER SIDE OF PROXYCHAINS


	IH>ssh user@BH1 -L 55201:192.168.1.10:22 -NT

banner grab 

	nc 127.0.0.1 52201
When you get onto a new box

	BPH1> <host enumeration>
 
"Host enumeration will set you free." -SSgt Woods

In order to do remote port forward, you must ssh on BPH1

	IH> ssh user@127.0.0.1 -p 52201

 Now that youre on BPH1

 	BPH1> ssh user@BH1int -R 52299:172.0.0.1:80 -NT

  When youre doing remote port forward start at high end and decrement by one as you go on

Port forward only bind to loopback 

	IH> ssh user@BH1 -L 52202:127.0.0.1:5299 -NT

 	IH> nc 127.0.0.1 52202

  To access FTP using Dynamic port forward

  	IH> ssh user@172.0.0.1:52201 -D 9050 -NT

make sure other  9050 tunnel is closed


   	IH> proxychains wget -r ftp://127.0.0.1
    
    			ftp 127.0.0.1


## Post Chow Lecture

ips are used to show relating pieces. NOT PART OF SYNTAX

	host>~$ (<user><ip>) -L <bind port>:(<tgt_ip>:<tgt_ip>) -NT

	host>~$ (<user><ip> -R <bind_port>):tgt_ip>:<tgt_port> -NT

	host>~$ (<user><ip>) -D 9050 -NT


 Steps

 nmap scan

 nc ports to verify services

 if ssh is identified, ssh to tgt

 host enumeration

 dynamic port forward

 map tunnel

 proxy chains wget -r

 proxy chains nc

 nc -znvw1 <ip> p-p p

if trying to forawrd traffic from a machine back to initial hos t use remote port forawrd

damien>ssh user@james-host-int -R 52299:127.0.0.1:22 -NT

on host machine make local port forward to james host 

ssh user@james-host-ext -L 52200:127.0.0.1:52299 -NT

MAP IT

on int host nc loopback to 52200

close connection with damians 22

# HAHAHAHAHAHAHAHAHA JUST KIDDING GET FREAKED ON NERD


ssh user@james-host-ext -L 52201:damien-host-ext :23 -NT 

nc 172.0.0.1 52201

ssh user@james-host-int -R 52299:127.0.0.1:22 -NT







