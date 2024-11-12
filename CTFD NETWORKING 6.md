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
