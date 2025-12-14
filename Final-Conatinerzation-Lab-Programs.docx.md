# **Lab Manual –Containerzation-Lab(1 to 10 Expts)**

**Experiment-1: Create Docker Image**

\-\>Login:RIT-ADMIN  
Password: rit@2025

1. ###### **Step: Create a folder Hello-world in Home folder**

\-\>open Terminal  
\-\>cd hello-world  
\-\>vim app.py

\#\# 1\. Create a simple Python program Make a file called \`app.py\`:

\`\`\`python  
print("Hello, World from Docker\!")  
\`\`\`

\-\>Save file with \-\>shift:wq

\-\>vim Dockerfile

2. ###### **Step. Write a Dockerfile**

Create a file named \`Dockerfile\` in the same folder:

\`\`\`dockerfile  
\# Use the official Python image as base FROM python:3.9-slim

\# Set working directory inside the container WORKDIR /app

\# Copy everything into /app COPY . /app

\# Run the Python program CMD \["python", "app.py"\]  
\`\`\`

Save the file-\> shift:wq

3. ###### **Step Build the Docker image**

Open a terminal in the folder and run:

\-◻docker build \-t hello-docker .

###### **Step 4\. Run the container**

Now run the image:

□  docker run hello-docker

![][image1] Output should be:

Hello, World from Docker\!

# **Experiment 2: Arithmetic Calculator in Docker**

#### **Objective:**

* Build a simple arithmetic calculator app using Python.  
* Dockerize the app and run it inside a container.

###### **Steps: 1\. calculator.py**

def calculator():

print("Simple Arithmetic Calculator")

a \= float(input("Enter first number: "))

b \= float(input("Enter second number: "))

print("Select operation:\\n1. Add\\n2. Subtract\\n3. Multiply\\n4. Divide") choice \= input("Enter choice (1/2/3/4): ")

if choice \== '1': print(f"Result: {a \+ b}")

elif choice \== '2': print(f"Result: {a \- b}")  
elif choice \== '3':

print(f"Result: {a \* b}") elif choice \== '4':  
if b \!= 0:

print(f"Result: {a / b}") else:  
print("Cannot divide by zero\!")

else:

print("Invalid choice\!")

if   name   \== " main ": calculator()

2. ###### **Step:Dokerfile**

\# Use Python lightweight base image FROM python:3.10-slim

\# Set working directory WORKDIR /app

\# Copy calculator code into container COPY calculator.py .

\# Run calculator when container starts CMD \["python", "calculator.py"\]

3. ###### **Build the Docker Image**

Open a terminal, go to the folder containing the two files, and run:

###### **docker build \-t arithmetic-calculator .**

4. **Run the Container (Interactive) docker run \-it arithmetic-calculator Output:**

Example Run (inside container) Simple Arithmetic Calculator Enter first number: 10  
Enter second number: 5 Select operation:

1. Add

2. Subtract

3. Multiply

4. Divide

Enter choice (1/2/3/4): 3 Result: 50.0

rit@rit:\~/Calculator$ sudo docker run \-it arithmetic-calculator Simple Arithmetic Calculator  
Enter first number: 20 Enter second number: 30 Select operation:

1. Add

2. Subtract

3. Multiply

4. Divide

Enter choice (1/2/3/4): 1 Result: 50.0

# **Experiment 3: Demonstrate CPU Delay (CPU Intensive Task in Docker)**

#### **Objective:**

* Show how to create CPU load inside a Docker container to demonstrate CPU delay or resource consumption.

#### **Steps:**

1. ###### **Create a CPU load Python script (cpuload.py):**

import time

print("Starting CPU-intensive task...") start \= time.time()

\# Run a CPU-heavy loop for \~30 seconds while time.time() \- start \< 30:  
x \= 0

for i in range(1000000): x \+= i \* i

print("Task completed\!")

2. ###### **Step :Doker Image**

\# Use official Python slim image FROM python:3.10-slim

\# Set working directory WORKDIR /app

\# Copy the Python script into container COPY cpuload.py .

\# Run the script

CMD \["python", "cpuload.py"\]

3. ###### **Build Docker Image**

   In the terminal, go to the folder containing these files and run:

   **\-\>docker build \-t cpu-delay .**

4. ###### **Run the Container**

Without CPU limit (uses full CPU available):

###### **docker run cpu-delay**

With CPU limit (only 50% of one CPU core):

###### **docker run \--cpus=".5" cpu-delay**

5. **Monitor CPU Usage** Open another terminal and run: **top**

###### **or htop**

**Output:**

Without limit → container uses high CPU.

With \--cpus=".5" → container is throttled and takes longer.

Output:Screenshots:   
rit@rit:\~/CPU-Delay$ docker run cpu-delay Starting CPU-intensive task...  
Task completed\!

rit@rit:\~/CPU-Delay$ docker run \--cpus=".5" cpu-delay Starting CPU-intensive task...  
Task completed\!

Open another terminal and type:

rit@rit:top

top \- 10:58:46 up 26 min, 1 user, load average: 0.37, 0.43, 0.34

Tasks: 340 total,  2 running, 338 sleeping,  0 stopped,  0 zombie

%Cpu(s): 0.9 us, 0.5 sy, 0.0 ni, 98.6 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st

MiB Mem : 15734.4 total,  9245.3 free,  2694.7 used,  3794.3 buff/cache

MiB Swap:  7629.0 total,  7629.0 free,	0.0 used. 12390.2 avail Mem

PID USER	PR NI	VIRT	RES	SHR S %CPU %MEM	TIME+ COMMAND

| 2104 rit | 20 | 0 6183600 315236 153532 S 11.3 2.0  1:35.90 gnome-shell |  |
| :---- | ----- | ----- | :---- |
|  2654 rit |  20 |  0 |  831736 64696 49292 R  5.2  0.4  0:19.80 gnome-terminal- |
| 2731 rit | 20 | 0 | 12.3g 608324 249648 S  1.7  3.8  1:10.70 firefox |
| 72 root | 20 | 0 | 0	0	0 S  0.9  0.0  0:02.15 ksoftirqd/9 |
| 164 root | 0 | \-20 | 0	0	0 I 0.9  0.0  0:03.33 kworker/u33:0-i915\_flip |

220 root	0 \-20	0	0	0 I  0.9  0.0  0:00.04 kworker/9:1H-events\_highpri

# **Experiment 4: Container Program – Factorial Calculator**

#### **Objective**

* To create a Python program that calculates the factorial of a number.  
  * To dockerize the program and run it inside a container.

###### **Steps**

1. Create Python Program (factorial.py)

def factorial(n):

return 1 if n \== 0 else n \* factorial(n-1)

if   name   \== "  main  ":

num \= int(input("Enter a number: ")) print(f"Factorial of {num} is {factorial(num)}")

2. ###### **Create Dockerfile**

FROM python:3.10-slim

\# Set working directory inside container WORKDIR /app

\# Copy factorial script into container COPY factorial.py .

\# Run factorial program when container starts CMD \["python", "factorial.py"\]

3. ###### **Build the Docker Image**

Open a terminal in the folder containing factorial.py and Dockerfile, then run:

docker build \-t factorial-calculator .

4. **Run the Container (Interactive Mode) docker run \-it factorial-calculator**

#### **Expected Outcome**

When the container starts, it will prompt for input:

###### **Enter a number: 5 Factorial of 5 is 120**

**Output Screenshots:**

**rit@rit:\~$ cd Factorial** rit@rit:\~/Factorial$ vim factorial.py rit@rit:\~/Factorial$ vim dockerfile

rit@rit:\~/Factorial$ docker build \-t factorial-calculator .

rit@rit:\~/Factorial$ docker run \-it factorial-calculator Enter a number: 4

Factorial of 4 is 24 rit@rit:\~/Factorial$ 

5. Experiment 5-Te create a Chart

   1. App.py:

import csv

def read\_csv(filename): students \= \[\]

with open(filename, newline='') as csvfile: reader \= csv.DictReader(csvfile)  
for row in reader:  
students.append((row\['Name'\], int(row\['Marks'\]))) return students

def draw\_bar\_chart(data):  
print("Student Marks Visualization\\n") max\_name\_len \= max(len(name) for name, \_ in data) max\_mark \= max(mark for \_, mark in data)

for name, mark in data:  
bar \= '█' \* (mark \* 50 // max\_mark) \# scale to max 50 chars  
print(f"{name.ljust(max\_name\_len)} | {bar} {mark}")

if   name  \== "  main  ":

students \= read\_csv("students.csv") draw\_bar\_chart(students)

2. Dockerfile:

\# Use official Python slim image FROM python:3.9-slim

\# Set working directory WORKDIR /app

\# Copy files

COPY app.py students.csv ./

\# Run the program

CMD \["python", "app.py"\]

Student.csv:

| Name | Marks |
| :---- | ----- |
| alice | 85 |
| shoba | 95 |
| hemanth | 100 |
| eye | 99 |

.**Note:Create a students.csv file and save it in folder chart**

it@rit:\~$ cd chart rit@rit:\~/chart$ vi app.py rit@rit:\~/chart$ vi dockerfile  
rit@rit:\~/chart$ docker build \-t chart-calculator .

rit@rit:\~/chart$ docker build \-t chart-calculator .

rit@rit:\~/chart$ docker run \-it chart-calculator

Student Marks Visualization

alice | ██████████████████████████████████████████ 85

shoba  | ███████████████████████████████████████████████

95

hemanth |

██████████████████████████████████████████████████ 100

eye	|

█████████████████████████████████████████████████ 99

rit@rit:\~/chart$ rit@rit:\~/chart$ vi app.py

### **Experiment 6: Environment Variables Passed to Container Python File:**

import os

print("=== Environment Variables Passed to Container \===\\n")

for key, value in os.environ.items(): print(f"{key} \= {value}")

**Dockerfile**  
FROM python:3.9-slim WORKDIR /app COPY env\_printer.py .  
CMD \["python", "env\_printer.py"\]

rit@rit:\~/Envt$ vi app.py rit@rit:\~/Env$ vi dockerfile

rit@rit:\~/Env$ docker build \-t Env-calculator . rit@rit:\~/Env$ docker run \-it Env-calculator

## **7\. Ping Simulation**

**Ping Program Without Internet:Program-11**

it@rit:\~$ cd message  
rit@rit:\~/message$ nano ping.py

**Python File:**  
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

**172.1.44.108 is not reachable**

### **Program-8-Prime Number-Checker**

rit@rit:\~/Prime-Number-Checker$ vi prime.py \# prime.py  
def is\_prime(n):  
if n \<= 1: return False  
for i in range(2, int(n \*\* 0.5) \+ 1): if n % i \== 0:  
return False return True

if   name   \== "  main  ":  
print("=== Prime Number Checker (Python in Docker) \===") num \= int(input("Enter a number: "))

if is\_prime(num):  
print(f"{num} is a Prime Number.") else:  
print(f"{num} is NOT a Prime Number.") rit@rit:\~/Prime-Number-Checker$ vi dockerfile

\# Use locally available Python base image FROM python:3.9-slim

\# Set working directory inside container WORKDIR /app

\# Copy the Python program into the container COPY prime.py .

\# Run the Python script CMD \["python", "prime.py"\]

rit@rit:\~/Prime-Number-Checker$ docker build \-t python-prime .

	0.0s rit@rit:\~/Prime-Number-Checker$ docker run \-it python-prime  
\=== Prime Number Checker (Python in Docker) \=== Enter a number: 45  
45 is NOT a Prime Number. rit@rit:\~/Prime-Number-Checker$

**Program-9**

###### **Step 1: Install Minikube (on Ubuntu)**

\# 1\. Update system packages sudo apt update \-y

\# 2\. Install curl if not already installed sudo apt install curl \-y

\# 3\. Download Minikube binary  
curl \-LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

\# 4\. Install Minikube  
sudo install minikube-linux-amd64 /usr/local/bin/minikube

###### **Step 2: Install kubectl (Kubernetes CLI)**

\# Download the latest stable kubectl binary  
curl \-LO "https://storage.googleapis.com/kubernetes-release/release/$(curl \-s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"

\# Make it executable chmod \+x kubectl

\# Move it to your PATH  
sudo mv kubectl /usr/local/bin/

###### **Step 3:Test installation:**

minikube version kubectl version \--client

**Step 4: Start Minikube**

**\# Start Minikube using Docker as driver (recommended) minikube start \--driver=docker**

**minikube status**

**Step 5: Create the Pod and Service file**  
rit@rit:minikube ssh docker pull nginx exit  
rit@rit:\~$ nano hello.yaml apiVersion: v1  
kind: Pod metadata:  
name: hello-pod labels:  
app: hello spec: containers:

\- name: hello-container image: nginx  
ports:  
\- containerPort: 80  
\---  
apiVersion: v1 kind: Service metadata:

name: hello-service spec:  
selector:  
app: hello type: NodePort ports:  
\- port: 80

targetPort: 80  
nodePort: 30007 Press ctr+x and save yes  
rit@rit:\~$ nano hello.yaml  
rit@rit:\~$ kubectl apply \-f hello.yaml pod/hello-pod created  
service/hello-service unchanged rit@rit:\~$ kubectl get pods

NAME	READY STATUS	RESTARTS AGE  
hello-deploy-55b5759b47-tknsj 0/1	ImagePullBackOff	0	4m26s hello-pod	0/1	ContainerCreating 0	17s  
rit@rit:\~$ minikube ip 192.168.49.2  
rit@rit:\~$ kubectl get pods  
NAME	READY STATUS	RESTARTS AGE  
hello-deploy-55b5759b47-tknsj 0/1	ImagePullBackOff 0	8m28s hello-pod	0/1	ImagePullBackOff 0	4m19s rit@rit:\~$ minikube ssh  
docker@minikube:\~$ docker pull nginx Using default tag: latest

cError response from daemon: Get "https://registry-1.docker.io/v2/": net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers) docker@minikube:\~$  
docker@minikube:\~$ docker@minikube:\~$ docker images

 docker@minikube:\~$ docker pull nginx  
Using default tag: latest  
latest: Pulling from library/nginx 38513bd72563: Pull complete 10d18f46ee87: Pull complete a8d825a0683a: Pull complete a131bc1d4bd5: Pull complete 3818929ac19f: Pull complete 1498b1cfda15: Pull complete c50c84d0ed4d: Pull complete

Digest: sha256:029d4461bd98f124e531380505ceea2072418fdf28752aa73b7b273ba3048903 Status: Downloaded newer image for nginx:latest  
docker.io/library/nginx:latest docker@minikube:\~$ docker images  
REPOSITORY	TAG	IMAGE ID	CREATED	SIZE  
nginx	latest	 657fdcd1c365 2 weeks ago	152MB registry.k8s.io/kube-apiserver				v1.34.0 90550c43ad2b 2 months ago 88MB registry.k8s.io/kube-proxy				v1.34.0 df0860106674 2 months ago 71.9MB registry.k8s.io/kube-scheduler					v1.34.0 46169d968e92 2 months ago 52.8MB registry.k8s.io/kube-controller-manager v1.34.0 a0af72f2ec6d 2 months ago 74.9MB registry.k8s.io/etcd		3.6.4-0 5f1f5298c888 3 months ago 195MB registry.k8s.io/pause			3.10.1	cd073f4c5f6a 4 months ago 736kB registry.k8s.io/coredns/coredns						v1.12.1 52546a367cc9 6 months ago 75MB gcr.io/k8s-minikube/storage-provisioner v5	6e38f40d628d 4 years ago	31.5MB docker@minikube:\~$

**in new terminal**

rit@rit:\~$ kubectl delete pod hello-pod kubectl delete deployment hello-deploy  
pod "hello-pod" deleted from default namespace deployment.apps "hello-deploy" deleted from default namespace rit@rit:\~$ nano hello.yaml

rit@rit:\~$ kubectl apply \-f hello.yaml pod/hello-pod created  
service/hello-service unchanged rit@rit:\~$ kubectl get pods  
NAME	READY STATUS	RESTARTS AGE  
hello-pod 1/1	Running 0	10s rit@rit:\~$ kubectl get svc

NAME	TYPE	CLUSTER-IP	EXTERNAL-IP PORT(S)	AGE  
hello-service NodePort	10.109.4.244 \<none\>		80:30007/TCP 12m kubernetes	ClusterIP 10.96.0.1	\<none\>	443/TCP	17m rit@rit:\~$

In browser:type [http://192.168.49.2:30007/](http://192.168.49.2:30007/)

output will be displayed:

**Welcome to nginx\!**

If you see this page, the nginx web server is successfully installed and working. Further configuration is required.

For online documentation and support please refer to nginx.org. Commercial support is available at nginx.com.

*Thank you for using nginx.*

## **Program-10: Simple Ubuntu Container with a Custom Script (Offline Compatible)**

##### **Step 1: Create a working folder**

mkdir mydockerapp cd mydockerapp

##### **Step 2: Create a small shell script**

Create a file named hello.sh nano hello.sh

Paste this:

\#\!/bin/bash

echo "	"

echo " Welcome to Docker Offline Demo\! "

echo " This script is running inside a container." echo "	"

Save and exit (Ctrl \+ O, Enter, Ctrl \+ X).

##### **Step 3: Create a Dockerfile**

nano Dockerfile

Paste this:

\# Use a basic Ubuntu image (should already exist in lab systems)

FROM ubuntu:latest

\# Set working directory WORKDIR /app

\# Copy script into container COPY hello.sh .

\# Give execute permission RUN chmod \+x hello.sh

\# Set the script to run when container starts CMD \["./hello.sh"\]

##### **Step 4: Build the image**

docker build \-t offline-demo .

If ubuntu:latest is already downloaded, this runs completely offline. Otherwise, ask the examiner if the base image is pre-pulled.

##### **Step 5: Run the container**

docker run offline-demo

##### **Output:**

Welcome to Docker Offline Demo\!

This script is running inside a container.

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAACOUlEQVR4XsWXTytFQRjGfQQfwUewoYvokpSFnZIsWEjHv5JIubdQSiJJRP6d4m6UEm6UrpAQsqEoFoqNIpQsZDF6boZz3pkxM0euU7/NnPe+zzPv+84956SlfV7dbjg9ulQc/mucqVDYGQ9lcN3kFV0u6o6uFrFU0LlcyBrncpgzE3K/DXgCetZK2dBmFRveqvbRFS8RkgWldSGfOW6INUxmZfoM9G+Us9hRRGDusCNpjCYKCjeAdvgMTOzW+4TdgzY2kKgIvPve9TIWPx1hifNZNpio1BvATrn42E5dYGHO7cMFe397+2J0uza5rjTgFafJbDm+jvvEASqBe1oDv+334kmfIG5sYGa/RUhoA8pMhcHL6+PXHCgNoPQ4CTSpKRg6CFFxML33vTGlgd9ydXcsCHtLz9EaQBnxI8AnV8fu5YIgDM5ut4XYHw3QMnp7p0I1dDiGyEfjfzSAXtFE2B1NwkGFZH3Hmqp61gbun2+EJAC7wz0aD2KHESHeyACQ7Ui2G/SXxgE6dBStAdm/GG0DRGgMwEmg+ShaAygfTextg+w+j5ENHUVrAKjaEGToKEYGZG3AGn3CcXAUaQ4VRgZUZZZB50OHkQEgKzXFZOgoxgZkbfACgyZDRzE2oGuD6dBRjA0AVRtsho5iZUDWBqzROBusDNA3HBxDGmOLlQGAxzH+evGKHWToKIKB9sUCIeiviKwUsqb5XL+BOjf7qTmWx1JB8rsQ4q7n08xxs2r4Ysrwfpz+5/UBJfL0jKYANnQAAAAASUVORK5CYII=>