# TASK 1

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



# ANSWER 

  467accfb25050296431008a1357eacb1
