# TASK 1


## FILTERING T1

sudo iptables -A INPUT -p tcp -m multiport --ports 22,23,3389 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp -m multiport --ports 22,23,3389 -m state --state NEW,ESTABLISHED -j ACCEPT


sudo iptables -t filter -P INPUT DROP
sudo iptables -t filter -P OUTPUT DROP
sudo iptables -t filter -P FORWARD DROP

sudo iptables -A INPUT -p icmp --icmp-type 8 -s 10.10.0.40 -j ACCEPT
sudo iptables -A INPUT -p icmp --icmp-type 8 -d 10.10.0.40 -j ACCEPT

sudo iptables -A OUTPUT -p icmp --icmp-type 8 -d 10.10.0.40 -j ACCEPT
sudo iptables -A OUTPUT -p icmp --icmp-type 8 -s 10.10.0.40 -j ACCEPT

sudo iptables -A INPUT -p icmp --icmp-type 0 -s 10.10.0.40 -j ACCEPT
sudo iptables -A OUTPUT -p icmp --icmp-type 0 -s 10.10.0.40 -j ACCEPT

sudo iptables -A OUTPUT -p icmp --icmp-type 0 -d 10.10.0.40 -j ACCEPT
sudo iptables -A INPUT -p icmp --icmp-type 0 -d 10.10.0.40 -j ACCEPT

sudo iptables -A INPUT -p tcp -m multiport --ports 4444, 6579 -j ACCEPT
sudo iptables -A OUTPUT -p tcp -m multiport --ports 4444, 6579 -j ACCEPT

sudo iptables -A INPUT -p udp -m multiport --ports 4444, 6579 -j ACCEPT
sudo iptables -A OUTPUT -p udp -m multiport --ports 4444, 6579 -j ACCEPT

sudo iptables -A INPUT -p tcp --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A INPUT -p tcp --sport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp --sport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT



### ANSWER 

  467accfb25050296431008a1357eacb1



  ## FILTERING T3

  sudo iptables -A INPUT -p tcp -m multiport --ports 22,23,3389 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp -m multiport --ports 22, 23, 3389 -m state --state NEW, ESTABLISHED -j ACCEPT


sudo iptables -t filter -P INPUT DROP
sudo iptables -t filter -P OUTPUT DROP
sudo iptables -t filter -P FORWARD DROP


sudo iptables -A INPUT -p tcp --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A INPUT -p tcp --sport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp --sport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT


### ANSWER

05e5fb96e2a117e01fc1227f1c4d664c


## FILTERING T2

### PROMPT 
```
NFTable Rule Definitions

NFTable: CCTC
Family: ip

Create input and output base chains with:
Hooks
Priority of 0
Policy as Accept

Allow New and Established traffic to/from via SSH, TELNET, and RDP

Change your chains to now have a policy of Drop

Allow ping (ICMP) requests (and reply) to and from the Pivot.

Allow ports 5050 and 5150 for both udp and tcp traffic to/from

Allow New and Established traffic to/from via HTTP

Once these steps have been completed and tested, go to Pivot and open up a netcat listener on port 9002 and wait up to 2 minutes for your flag. If you did not successfully accomplish the tasks above, then you will not receive the flag.
```
sudo nft add table ip CCTC

sudo nft add chain ip CCTC INPUT { type filter hook input priority 0 \; policy accept \; }
sudo nft add chain ip CCTC OUTPUT { type filter hook output priority 0 \; policy accept \; }


sudo nft insert rule ip CCTC INPUT tcp dport { 22, 23, 3389 } ct state { new, established } accept 
sudo nft insert rule ip CCTC OUTPUT tcp dport { 22, 23, 3389 } ct state { new, established } accept 
sudo nft insert rule ip CCTC OUTPUT tcp sport { 22, 23, 3389 } ct state { new, established } accept 
sudo nft insert rule ip CCTC INPUT tcp sport { 22, 23, 3389 } ct state { new, established } accept

sudo nft chain ip CCTC INPUT { \; policy drop \; }
sudo nft chain ip CCTC OUTPUT { \; policy drop \; }


sudo nft insert rule ip CCTC INPUT icmp type 8 ip  saddr 10.10.0.40 accept
sudo nft insert rule ip CCTC INPUT icmp type 0 ip  saddr 10.10.0.40 accept
sudo nft insert rule ip CCTC OUTPUT icmp type 0 ip  saddr 10.10.0.40 accept
sudo nft insert rule ip CCTC OUTPUT icmp type 8 ip  saddr 10.10.0.40 accept
sudo nft insert rule ip CCTC OUTPUT icmp type 8 ip  daddr 10.10.0.40 accept
sudo nft insert rule ip CCTC OUTPUT icmp type 0 ip  daddr 10.10.0.40 accept
sudo nft insert rule ip CCTC INPUT icmp type 0 ip  daddr 10.10.0.40 accept
sudo nft insert rule ip CCTC INPUT icmp type 8 ip  daddr 10.10.0.40 accept



sudo nft insert rule ip CCTC INPUT tcp dport { 5050, 5150 }  accept
sudo nft insert rule ip CCTC INPUT tcp sport { 5050, 5150 }  accept
sudo nft insert rule ip CCTC OUTPUT tcp sport { 5050, 5150 }  accept
sudo nft insert rule ip CCTC OUTPUT tcp dport { 5050, 5150 }  accept

sudo nft insert rule ip CCTC INPUT tcp dport { 80 } ct state { new, established } accept
sudo nft insert rule ip CCTC INPUT tcp sport { 80 } ct state { new, established } accept
sudo nft insert rule ip CCTC OUTPUT tcp sport { 80 } ct state { new, established } accept
sudo nft insert rule ip CCTC OUTPUT tcp dport { 80 } ct state { new, established } accept


ANSWER:

9f7a33941828bdafd2755fd20176cdf4


## FILTERING VALIDATION

```
For verification (only) of your IPTables and NFTables rules. This is NOT required for the flag:

Pivot can SSH into all three targets

Pivot can ping T1 and T2 but not T3

T1, T2 andT3 should not be able to PING each other

Pivot can access all three targets via HTTP

Monitor via TCPDump on T3 for web traffic from outside the network

Monitor via TCPDump on T1 for traffic on the allowed high ports

Monitor via TCPDump on T2 for traffic on the allowed high ports


To get the Validation FLAG:

Once you have received the flag for T1, T2, and T3, go to Pivot and perform an md5sum on the combination of T1 flag, T2 flag, and T3 flag combined and separated by underscores.

For example:

echo "T1flag_T2flag_T3flag" | md5sum

Update the Stream Socket Message Sender script created in Networking - 2 - Socket Creation and Packet Manipulation.

Send the result of the md5sum of all three flags separated by underscores to the same IP address and port (IP 172.16.1.15 Port 5309) to receive your flag
```
echo 467accfb25050296431008a1357eacb1_9f7a33941828bdafd2755fd20176cdf4_05e5fb96e2a117e01fc1227f1c4d664c | md5sum

953e720e688941b15b72c098022c51c3

nano socks.py

"Edit message from 'Jenny' to  953e720e688941b15b72c098022c51c3"

./socks.py 

### ANSWER 

d3b88e04de1e76482a1972f36734a7d8


# TASK 2
## NAT T5

### PROMPT
```
IPTable Rule Definitions

On T1 edit the /proc/sys/net/ipv4/ip_forward file to enable IP Forwarding. Change the value from 0 to 1.

On T1 change the FORWARD policy back to ACCEPT.

Configure POSTROUTING chain to translate T5 IP address to T1 (Create the rule by specifying the Interface information first then Layer 3)

Once these steps have been completed and tested, go to Pivot and open up a netcat listener on port 9004 and wait up to 2 minutes for your flag. If you did not successfully accomplish the tasks above, then you will not receive the flag.
```
cd /proc/sys/net/core/ipv4
nano ip_forward
*change 0 to 1*

sudo iptables -t filter -P FORWARD ACCEPT

sudo iptables -t nat -A POSTROUTING -o eth0 -s 192.168.1.10 -j SNAT --to 172.16.82.106

### ANSWER

0c2ca80fad4accccce3bcecec1d238ce

## NAT T6


```
NFTable Rule Definitions

NFTable: NAT
Family: ip

On T2 edit the /proc/sys/net/ipv4/ip_forward file to enable IP Forwarding. Change the value from 0 to 1.

Create POSTROUTING and PREROUTING base chains with:
Hooks
Priority of 0
No Policy Needed

Configure POSTROUTING chain to translate T6 IP address to T2 (Create the rule by specifying the Interface information first then Layer 3)

Once these steps have been completed and tested, go to Pivot and open up a netcat listener on port 9005 and wait up to 2 minutes for your flag. If you did not successfully accomplish the tasks above, then you will not receive the flag.
```
sudo nft add table ip NAT

sudo nft add chain ip NAT POSTROUTING { type nat hook postrouting priority 0 \; }
sudo nft add chain ip NAT PREROUTING { type nat hook prerouting priority 0 \; }
sudo nft add rule ip NAT POSTROUTING ip saddr 192.168.3.30 oif eth0 snat 172.16.82.112

### ANSWER 

be33fe60229f8b8ee22931a3820d30ac






