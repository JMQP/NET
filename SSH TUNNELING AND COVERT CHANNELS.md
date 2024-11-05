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





























