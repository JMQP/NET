# LOCAL PORT FORWARDING

ssh -p <optional alt port> <user>@<server ip> -L <local bind port>:<tgt ip>:<tgt port> -NT

or

ssh -L <local bind port>:<tgt ip>:<tgt port> -p <alt port> <user>@<server ip> -NT

## LOCAL PORT FORWARD TO LOCALHOST OF SERVER
Internet_Host:

    ssh student@172.16.1.15 -L 1122:localhost:22
or

	ssh -L 1122:localhost:22 student@172.16.1.15

Internet_Host:

	ssh student@localhost -p 1122
	Blue_DMZ_Host-1~$

## LOCAL PORT FORWARD TO LOCALHOST OF SERVER

![local1](https://github.com/user-attachments/assets/c864ba0d-85c9-4116-a839-a9be062fdc0b)

Internet_Host:

	ssh student@172.16.1.15 -L 1123:localhost:23

or


	ssh -L 1123:localhost:23 student@172.16.1.15


Internet_Host:
	
 	telnet localhost 1123
	Blue_DMZ_Host-1~$

![local2](https://github.com/user-attachments/assets/5d85317a-beca-4dc5-bff4-9d616bde02f0)

Internet_Host:

	ssh student@172.16.1.15 -L 1180:localhost:80

or

	ssh -L 1180:localhost:80 student@172.16.1.15

Internet_Host:
	
 	firefox http://localhost:1180
	{Webpage of Blue_DMZ_Host-1}
![local3](https://github.com/user-attachments/assets/608547c1-27f5-4c3e-bd2e-95bbb1475a34)

## LOCAL PORT FORWARD TO REMOTE TARGET VIA SERVER


Internet_Host:

	ssh student@172.16.1.15 -L 2222:172.16.40.10:22

or

	ssh -L 2222:172.16.40.10:22 student@172.16.1.15

Internet_Host:

	ssh student@localhost -p 2222

	Blue_INT_DMZ_Host-1~$

![local4](https://github.com/user-attachments/assets/80f7f287-0b75-4781-8db7-d8245c3c1fd9)


Internet_Host:

	ssh student@172.16.1.15 -L 2223:172.16.40.10:23

or

	ssh -L 2223:172.16.40.10:23 student@172.16.1.15

Internet_Host:

	telnet localhost 2223

	Blue_INT_DMZ_Host-1~$

![local5](https://github.com/user-attachments/assets/c1456f86-b97c-42e9-ba94-2405c45d876b)


Internet_Host:

	ssh student@172.16.1.15 -L 2280:172.16.40.10:80

or

	ssh -L 2280:172.16.40.10:80 student@172.16.1.15

Internet_Host:

	firefox http://localhost:2280

	{Webpage of Blue_INT_DMZ_Host-1}
![local6](https://github.com/user-attachments/assets/6bf43f14-252b-4bcc-8752-bcc4c5187cb3)

## FORWARD THROUGH TUNNEL

Internet_Host:

	ssh student@172.16.1.15 -L 2222:172.16.40.10:22

	ssh student@localhost -p 2222 -L 3322:172.16.82.106:22

Internet_Host:

	ssh student@localhost -p 3322

	Blue_Host-1~$

 
![doublelocal1](https://github.com/user-attachments/assets/9cb4a125-682d-4cf5-b613-2842714a8940)

Internet_Host:

	ssh student@172.16.1.15 -L 2222:172.16.40.10:22

	ssh student@localhost -p 2222 -L 3323:172.16.82.106:23

Internet_Host:

	telnet localhost 3323

	Blue_Host-1~$

![doublelocal2](https://github.com/user-attachments/assets/42649756-5a5d-4e0f-ae91-80bdd40cedc8)


Internet_Host:

	ssh student@172.16.1.15 -L 2222:172.16.40.10:22

	ssh student@localhost -p 2222 -L 3380:172.16.82.106:80

Internet_Host:

	firefox http://localhost:3380

	{Webpage of Blue_Host-1}

![doublelocal3](https://github.com/user-attachments/assets/15f90b53-de5d-4027-99b1-4ec170e9e856)

# DYNAMIC PORT FORWARDING

	ssh <user>@<server ip> -p <alt port> -D <port> -NT

or

	ssh -D <port> -p <alt port> <user>@<server ip> -NT

Proxychains default port is 9050

Creates a dynamic socks4 proxy that interacts alone, or with a previously established remote or local port forward.

Allows the use of scripts and other userspace programs through the tunnel.

## SSH DYNAMIC PORT FORWARDING 1-STEP

Internet_Host:

	ssh student@172.16.1.15 -D 9050

or

	ssh -D 9050 student@172.16.1.15
![dynamic1](https://github.com/user-attachments/assets/81e4ee4c-a500-4d33-aab6-5a48dfc27edd)


### Proxychains Options
```
proxychains ./scan.sh
proxychains nmap -Pn 172.16.40.0/27 -p 21-23,80
proxychains ssh student@172.16.40.10
proxychains telnet 172.16.40.10
proxychains wget -r http://172.16.40.10
proxychains wget -r ftp://172.16.40.10
```

## SSH DYNAMIC PORT FORWARDING 2-STEP

Internet_Host:

	ssh student@172.16.1.15 -L 2222:172.16.40.10:22

or

	ssh -L 2222:172.16.40.10:22 student@172.16.1.15

Internet_Host:

	ssh student@localhost -p 2222 -D 9050

or

	ssh -D 9050 student@localhost -p 2222

![dynamic2](https://github.com/user-attachments/assets/c179dd22-aa7a-459e-a2e2-a463c86790b1)


## Remote Port Forwarding


	ssh -p <optional alt port> <user>@<server ip> -R <remote bind port>:<tgt ip>:<tgt port> -NT

or

	ssh -R <remote bind port>:<tgt ip>:<tgt port> -p <alt port> <user>@<server ip> -NT

### REMOTE PORT FORWARDING FROM LOCALHOST OF CLIENT

Blue_DMZ_Host-1:

	ssh student@10.10.0.40 -R 4422:localhost:22

or

	ssh -R 4422:localhost:22 student@10.10.0.40

Internet_Host:

	ssh student@localhost -p 4422

	Blue_DMZ_Host-1~$


![remote1](https://github.com/user-attachments/assets/efb317fe-ac3c-4f10-a995-6a6afc3a9877)


Blue_DMZ_Host-1:

	ssh student@10.10.0.40 -R 4423:localhost:23

or

	ssh -R 4423:localhost:23 student@10.10.0.40

Internet_Host:

	telnet localhost 4423

	Blue_DMZ_Host-1~$


![remote2](https://github.com/user-attachments/assets/81811e07-b849-49cf-b9bf-a14ba1a52a1e)


Blue_DMZ_Host-1:

	ssh student@10.10.0.40 -R 4480:localhost:80

or

	ssh -R 4480:localhost:80 student@10.10.0.40

Internet_Host:

	firefox http://localhost:4480

	{Webpage of Blue_DMZ_Host-1}

![remote3](https://github.com/user-attachments/assets/56640180-a737-408d-9b33-457e8d5ba4d9)


Blue_DMZ_Host-1:

	ssh student@10.10.0.40 -R 5522:172.16.40.10:22

or

	ssh -R 5522:172.16.40.10:22 student@10.10.0.40

Internet_Host:

	ssh student@localhost -p 5522

	Blue_INT_DMZ_Host-1~$

![remote4](https://github.com/user-attachments/assets/b82f2924-aa1e-4a2e-8f48-b3b785d95e27)


## REMOTE PORT FORWARDING TO REMOTE TARGET VIA CLIENT

Blue_DMZ_Host-1:

	ssh student@10.10.0.40 -R 5523:172.16.40.10:23

or

	ssh -R 5523:172.16.40.10:23 student@10.10.0.40

Internet_Host:

	telnet localhost 5523

	Blue_INT_DMZ_Host-1~$
![remote5](https://github.com/user-attachments/assets/11c3522a-a42e-4c11-81b8-e47b90785d47)


Blue_DMZ_Host-1:

	ssh student@10.10.0.40 -R 5580:172.16.40.10:80

or

	ssh -R 5580:172.16.40.10:80 student@10.10.0.40

Internet_Host:

	firefox http://localhost:5580

	{Webpage of Blue_INT_DMZ_Host-1}
![remote6](https://github.com/user-attachments/assets/ac709301-a7c9-4de9-9fb7-c5f9a18d3fb1)

## COMBINING LOCAL AND REMOTE PORT FORWARDING


Internet_Host:

	ssh student@172.16.1.15 -L 2223:172.16.40.10:23 -NT

or

	ssh -L 2223:172.16.40.10:23 student@172.16.1.15 -NT

Internet_Host:

	telnet localhost 2223

	Blue_INT_DMZ_Host-1~$


##  BRIDGING LOCAL AND REMOTE PORT FORWARDING


Blue_INT_DMZ_Host-1:

	ssh student@172.16.1.15 -R 1122:localhost:22

or

	ssh -R 1122:localhost:22 student@172.16.1.15


 Internet_Host:

	ssh student@172.16.1.15 -L 2222:localhost:1122

or

	ssh -L 2222:localhost:1122 student@172.16.1.15

Internet_Host:

	ssh student@localhost -p 2222 -D 9050

or

	ssh -D 9050 student@localhost -p 2222 


![bridge](https://github.com/user-attachments/assets/b4016976-f4cf-493b-9d7d-a77896efea80)


# PERFORM SSH PRACTICE


## SCAN FIRST PIVOT

![tp1](https://github.com/user-attachments/assets/a26e2b45-9c5e-426a-9827-d5e374d7dab4)

## FIRST PIVOT EXTERNAL ACTIVE RECON

![tp2](https://github.com/user-attachments/assets/66f44b13-60ae-46ef-8520-11749c3d14a4)

## ENUMERATE FIRST PIVOT

![tp3](https://github.com/user-attachments/assets/66032c11-d43d-495b-8924-d86552dd0c91)

## SCAN SECOND PIVOT

![tp4](https://github.com/user-attachments/assets/5cab3283-ca34-47e4-a4d1-2ea0b41845c1)

## ENUMERATE SECOND PIVOT

![tp5](https://github.com/user-attachments/assets/fcd5175b-1a39-430d-a3f2-0897f576ea48)


## SCAN THIRD PIVOT

![tp6](https://github.com/user-attachments/assets/9257b3c1-7080-49e0-b55b-9b4aa0475ae6)

## ENUMERATE THIRD PIVOT

![tp7](https://github.com/user-attachments/assets/fde9e6fa-93ca-4d8c-980d-e4e8ab61501a)

## SCAN FORTH PIVOT

![tp8](https://github.com/user-attachments/assets/803fe3f4-239a-4172-85ff-3b480c2f20b1)

## ENUMERATE FORTH PIVOT
![tp9](https://github.com/user-attachments/assets/1aceb348-622d-41c5-a8d0-8d7bebfb8f02)










