Here are the extracted code snippets from the file:

**Experiment 1: Hello World Docker App**
- `app.py`
```python
print("Hello, World from Docker!")
```
- `Dockerfile`
```
FROM python:3.9-slim
WORKDIR /app
COPY . /app
CMD ["python", "app.py"]
```

**Experiment 2: Arithmetic Calculator in Docker**
- `calculator.py`
```python
def calculator():
    print("Simple Arithmetic Calculator")
    a = float(input("Enter first number: "))
    b = float(input("Enter second number: "))
    print("Select operation:")
    print("1. Add")
    print("2. Subtract")
    print("3. Multiply")
    print("4. Divide")
    choice = input("Enter choice (1/2/3/4): ")
    if choice == '1':
        print(f"Result: {a + b}")
    elif choice == '2':
        print(f"Result: {a - b}")
    elif choice == '3':
        print(f"Result: {a * b}")
    elif choice == '4':
        if b != 0:
            print(f"Result: {a / b}")
        else:
            print("Cannot divide by zero!")
    else:
        print("Invalid choice!")

if __name__ == "__main__":
    calculator()
```
- `Dockerfile`
```
FROM python:3.10-slim
WORKDIR /app
COPY calculator.py .
CMD ["python", "calculator.py"]
```

**Experiment 3: CPU Delay Demo in Docker**
- `cpuload.py`
```python
import time
print("Starting CPU-intensive task...")
start = time.time()
while time.time() - start < 30:
    x = 0
    for i in range(1000000):
        x += i
print("Task completed!")
```
- `Dockerfile`
```
FROM python:3.10-slim
WORKDIR /app
COPY cpuload.py .
CMD ["python", "cpuload.py"]
```

**Experiment 4: Factorial Calculator in Docker**
- `factorial.py`
```python
def factorial(n):
    return 1 if n == 0 else n * factorial(n - 1)

if __name__ == "__main__":
    num = int(input("Enter a number: "))
    print(f"Factorial of {num} is {factorial(num)}")
```
- `Dockerfile`
```
FROM python:3.10-slim
WORKDIR /app
COPY factorial.py .
CMD ["python", "factorial.py"]
```

**Experiment 5: Student Marks Chart**
- `app.py`
```python
import csv

def readcsv(filename):
    students = []
    with open(filename, newline='') as csvfile:
        reader = csv.DictReader(csvfile)
        for row in reader:
            students.append((row['Name'], int(row['Marks'])))
    return students

def drawbarchart(data):
    print("Student Marks Visualization")
    maxnamelen = max(len(name) for name, _ in data)
    maxmark = max(mark for _, mark in data)
    for name, mark in data:
        bar = "#" * (mark * 50 // maxmark)  # scale to max 50 chars
        print(f"{name.ljust(maxnamelen)}: {bar} {mark}")

if __name__ == "__main__":
    students = readcsv("students.csv")
    drawbarchart(students)
```
- `Dockerfile`
```
FROM python:3.9-slim
WORKDIR /app
COPY app.py students.csv .
CMD ["python", "app.py"]
```
- `students.csv`
```
Name,Marks
alice,85
shoba,95
hemanth,100
eye,99
```

**Experiment 6: Display Environment Variables**
- `envprinter.py`
```python
import os
print("Environment Variables Passed to Container")
for key, value in os.environ.items():
    print(f"{key}: {value}")
```
- `Dockerfile`
```
FROM python:3.9-slim
WORKDIR /app
COPY envprinter.py .
CMD ["python", "envprinter.py"]
```


## Lab 6A — Fibonacci Series Generator (from Containerization_Lab_Manual_Experiments_1_to_6_README.md)

Python file (app.py)
```python
n = int(input("Enter number of terms: "))
a, b = 0, 1
print("Fibonacci Series:")
for i in range(n):
    print(a, end=" ")
    a, b = b, a + b
print()
```

Dockerfile
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . /app
CMD ["python", "app.py"]
```

Commands to build and run
```bash
docker build -t fibonacci-app .
docker run -it fibonacci-app
```

---

## Lab 6B — Environment Variables Printer

Python file (env_printer.py)
```python
import os
print("Environment Variables Passed to Container")
for key, value in os.environ.items():
    print(f"{key}: {value}")
```

Dockerfile
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY envprinter.py .
CMD ["python", "envprinter.py"]
```

Commands to build and run
```bash
docker build -t Env-calculator .
docker run -it Env-calculator
```

---

## Lab 7 — Ping Simulation / Ping Program (ping.py)

Python file (ping.py)
```python
import os
import sys

if len(sys.argv) != 2:
    print("Usage: python ping.py <hostname_or_ip>")
    sys.exit(1)

host = sys.argv[1]

response = os.system(f"ping -c 4 {host}")

if response == 0:
    print(f"{host} is reachable")
else:
    print(f"{host} is not reachable")
```

Dockerfile
```dockerfile
FROM python:3.9-alpine

# Alpine already contains BusyBox ping by default
COPY ping.py /ping.py
ENTRYPOINT ["python", "/ping.py"]
```

Commands to build and run (as shown in the lab files)
```bash
sudo docker build -t ping .
sudo docker run ping
sudo docker run ping google.com
# or (non-sudo) if your user can access Docker:
docker build -t ping .
docker run ping google.com
```

---

## Lab 8 — Prime Number Checker (prime.py)

Python file (prime.py)
```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

if __name__ == "__main__":
    print("=== Prime Number Checker (Python in Docker) ===")
    num = int(input("Enter a number: "))

    if is_prime(num):
        print(f"{num} is a Prime Number.")
    else:
        print(f"{num} is NOT a Prime Number.")
```

Dockerfile
```dockerfile
# Use locally available Python base image
FROM python:3.9-slim
WORKDIR /app
COPY prime.py .
CMD ["python", "prime.py"]
```

Commands to build and run
```bash
docker build -t python-prime .
docker run -it python-prime
```

---

## Lab 9 — Minikube / Kubernetes Example (hello pod & service)

Files referenced: hello.yaml (manifest)

Example hello.yaml contents (as created in the lab)
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-pod
  labels:
    app: hello
spec:
  containers:
  - name: hello-container
    image: nginx
    ports:
    - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: hello-service
spec:
  selector:
    app: hello
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30007
```

Commands used in the lab to install/start and deploy
```bash
# Install Minikube (example steps shown in lab)
sudo apt update -y
sudo apt install curl -y
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Install kubectl
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

# Start minikube (Docker driver)
minikube start --driver=docker
minikube status

# Create & apply pod + service
kubectl apply -f hello.yaml

# Check pods & services
kubectl get pods
kubectl get svc

# Get minikube IP and browse
minikube ip
# then open in browser:
# http://<MINIKUBE_IP>:30007/
```

---

## Lab 10 — Simple Ubuntu Container with a Custom Script (hello.sh)

Shell script (hello.sh)
```bash
#!/bin/bash

echo "	"

echo " Welcome to Docker Offline Demo! "

echo " This script is running inside a container."
echo "	"
```

Dockerfile
```dockerfile
# Use a basic Ubuntu image (should already exist in lab systems)
FROM ubuntu:latest
WORKDIR /app
COPY hello.sh .
RUN chmod +x hello.sh
CMD ["./hello.sh"]
```

Commands to build and run
```bash
docker build -t offline-demo .
docker run offline-demo
```

---

## Lab 11 — Ping Program (Program-11) — (duplicate / reaffirmation of Lab 7)

(The repository contains a separate "Ping Program-11" file; contents are the same program and Dockerfile as shown in Lab 7. Repeating here for completeness.)

Python file (ping.py) — same as Lab 7
```python
import os
import sys

if len(sys.argv) != 2:
    print("Usage: python ping.py <hostname_or_ip>")
    sys.exit(1)

host = sys.argv[1]

response = os.system(f"ping -c 4 {host}")

if response == 0:
    print(f"{host} is reachable")
else:
    print(f"{host} is not reachable")
```

Dockerfile — same as Lab 7
```dockerfile
FROM python:3.9-alpine
# Alpine already contains BusyBox ping by default
COPY ping.py /ping.py
ENTRYPOINT ["python", "/ping.py"]
```

Commands
```bash
sudo docker build -t ping .
sudo docker run ping google.com
```

---

## Lab 12 — Temperature Converter (temp.py)

Python file (temp.py)
```python
def c_to_f(c):
    return (c * 9/5) + 32

def f_to_c(f):
    return (f - 32) * 5/9

if __name__ == "__main__":
    print("=== Temperature Converter (Docker Offline) ===")
    print("1. Celsius to Fahrenheit")
    print("2. Fahrenheit to Celsius")
      
    choice = input("Enter choice (1 or 2): ")

    if choice == "1":
        c = float(input("Enter Celsius: "))
        print("Fahrenheit =", c_to_f(c))
    elif choice == "2":
        f = float(input("Enter Fahrenheit: "))
        print("Celsius =", f_to_c(f))
    else:
        print("Invalid choice!")
```

Dockerfile
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY temp.py .
CMD ["python", "temp.py"]
```

Commands to build and run
```bash
docker build -t temp-converter .
docker run -it temp-converter
```

---

