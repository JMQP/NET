# CTF DOMAIN

http://10.50.23.214:8000


# Student Guide

https://net.cybbh.io/public/networking/latest/

# Miro Whiteboard

https://miro.com/app/board/o9J_klSqCSY=/


# Task 3 

sudo tcpdump -n "tcp[2:2] <= 1023 || udp[2:2] <= 1023" -r "/home/activity_resources/pcaps/BPFCheck.pcap" | wc -l
