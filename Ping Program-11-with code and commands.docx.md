  
**Ping Program Without Internet:Program-11**

it@rit:\~$ cd message  
rit@rit:\~/message$ nano ping.py

import os  
import sys

if len(sys.argv) \!= 2:  
    print("Usage: python ping.py \<hostname\_or\_ip\>")  
    sys.exit(1)

host \= sys.argv\[1\]

response \= os.system(f"ping \-c 4 {host}")

if response \== 0:  
    print(f"{host} is reachable")  
else:  
    print(f"{host} is not reachable")

rit@rit:\~/message$ vim Dockerfile

FROM python:3.9-alpine

\# Alpine already contains BusyBox ping by default

COPY ping.py /ping.py

ENTRYPOINT \["python", "/ping.py"\]

rit@rit:\~/CPU-Delay$ sudo docker pull python:3..9-alpine  
\[sudo\] password for rit:  
rit@rit:\~/CPU-Delay$ ls  
cpuload.py  Dockerfile  Factorial  
rit@rit:\~/CPU-Delay$ docker save \-o python\_3.10\_slim.tar python:3. 9-alpine  
permission denied while trying to connect to the docker API at unix:///var/run/docker.sock  
rit@rit:\~/CPU-Delay$  sudo docker save \-o python\_3.10\_slim.tar python:3. 9-alpine

rit@rit:\~/CPU-Delay$ sudo chmod 777 python\_9-alpine.tar  
rit@rit:\~/CPU-Delay$ sudo docker build \-t ping .

rit@rit:\~/message$ sudo docker build \-t ping .  
\[sudo\] password for rit: 

rit@rit:\~/message$ sudo docker run ping  
Usage: python ping.py \<hostname\_or\_ip\>  
rit@rit:\~/message$ sudo docker run ping google.com  
PING google.com (142.251.223.238): 56 data bytes  
64 bytes from 142.251.223.238: seq=0 ttl=113 time=6.157 ms  
64 bytes from 142.251.223.238: seq=1 ttl=113 time=6.583 ms  
64 bytes from 142.251.223.238: seq=2 ttl=113 time=7.338 ms  
64 bytes from 142.251.223.238: seq=3 ttl=113 time=6.163 ms

\--- google.com ping statistics \---  
4 packets transmitted, 4 packets received, 0% packet loss  
round-trip min/avg/max \= 6.157/6.560/7.338 ms  
google.com is reachable  
rit@rit:\~/message$ if config  
\> ^C  
rit@rit:\~/message$ ifconfig  
br-4045742296a8: flags=4099\<UP,BROADCAST,MULTICAST\>  mtu 1500  
        inet 172.18.0.1  netmask 255.255.0.0  broadcast 172.18.255.255  
        ether 2e:35:0b:6d:35:db  txqueuelen 0  (Ethernet)  
        RX packets 0  bytes 0 (0.0 B)  
        RX errors 0  dropped 0  overruns 0  frame 0  
        TX packets 0  bytes 0 (0.0 B)  
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

br-5a64d02fef70: flags=4099\<UP,BROADCAST,MULTICAST\>  mtu 1500  
        inet 192.168.49.1  netmask 255.255.255.0  broadcast 192.168.49.255  
        ether 0e:79:9d:9d:79:6b  txqueuelen 0  (Ethernet)  
        RX packets 0  bytes 0 (0.0 B)  
        RX errors 0  dropped 0  overruns 0  frame 0  
        TX packets 0  bytes 0 (0.0 B)  
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

br-5fc3b57c80ee: flags=4099\<UP,BROADCAST,MULTICAST\>  mtu 1500  
        inet 172.20.0.1  netmask 255.255.0.0  broadcast 172.20.255.255  
        ether 62:c1:73:20:a3:b0  txqueuelen 0  (Ethernet)  
        RX packets 0  bytes 0 (0.0 B)  
        RX errors 0  dropped 0  overruns 0  frame 0  
        TX packets 0  bytes 0 (0.0 B)  
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

br-a2590a68f2b3: flags=4099\<UP,BROADCAST,MULTICAST\>  mtu 1500  
        inet 172.19.0.1  netmask 255.255.0.0  broadcast 172.19.255.255  
        ether 7e:96:12:1c:32:ee  txqueuelen 0  (Ethernet)  
        RX packets 0  bytes 0 (0.0 B)  
        RX errors 0  dropped 0  overruns 0  frame 0  
        TX packets 0  bytes 0 (0.0 B)  
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

docker0: flags=4099\<UP,BROADCAST,MULTICAST\>  mtu 1500  
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255  
        inet6 fe80::d070:11ff:fe12:43cb  prefixlen 64  scopeid 0x20\<link\>  
        ether d2:70:11:12:43:cb  txqueuelen 0  (Ethernet)  
        RX packets 14  bytes 812 (812.0 B)  
        RX errors 0  dropped 0  overruns 0  frame 0  
        TX packets 12  bytes 1172 (1.1 KB)  
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eno1: flags=4163\<UP,BROADCAST,RUNNING,MULTICAST\>  mtu 1500  
        inet 172.1.44.107  netmask 255.255.254.0  broadcast 172.1.45.255  
        inet6 fe80::70ab:f57:9b2d:d237  prefixlen 64  scopeid 0x20\<link\>  
        ether d8:bb:c1:e6:01:1b  txqueuelen 1000  (Ethernet)  
        RX packets 486942  bytes 576216337 (576.2 MB)  
        RX errors 0  dropped 0  overruns 0  frame 0  
        TX packets 24156  bytes 7091836 (7.0 MB)  
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0  
        device interrupt 16  memory 0xb1200000-b1220000  

lo: flags=73\<UP,LOOPBACK,RUNNING\>  mtu 65536  
        inet 127.0.0.1  netmask 255.0.0.0  
        inet6 ::1  prefixlen 128  scopeid 0x10\<host\>  
        loop  txqueuelen 1000  (Local Loopback)  
        RX packets 1795  bytes 189361 (189.3 KB)  
        RX errors 0  dropped 0  overruns 0  frame 0  
        TX packets 1795  bytes 189361 (189.3 KB)  
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

rit@rit:\~/message$ sudo docker run ping 172.1.44.108  
PING 172.1.44.108 (172.1.44.108): 56 data bytes

\--- 172.1.44.108 ping statistics \---  
4 packets transmitted, 0 packets received, 100% packet loss  
172.1.44.108 is not reachable