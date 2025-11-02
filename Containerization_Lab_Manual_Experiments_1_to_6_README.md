# Lab Manual – Containerization (Experiments 1 to 6)

**Login:**
```
RIT-ADMIN
Password: rit@2025
```

---

## **Experiment 1: Hello World**
```bash
cd ~
mkdir Hello-world
cd Hello-world
vim app.py
```
**app.py**
```python
print("Hello, World from Docker!")
```
**Dockerfile**
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . /app
CMD ["python", "app.py"]
```
**Commands:**
```bash
docker build -t hello-docker .
docker run hello-docker
```

---

## **Experiment 2: Arithmetic Calculator**
**app.py**
```python
def calculator():
    print("Simple Arithmetic Calculator")
    a = float(input("Enter first number: "))
    b = float(input("Enter second number: "))
    print("Select operation:\n1. Add\n2. Subtract\n3. Multiply\n4. Divide")
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
**Dockerfile**
```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY app.py .
CMD ["python", "app.py"]
```
**Commands:**
```bash
docker build -t arithmetic-calculator .
docker run -it arithmetic-calculator
```

---

## **Experiment 3: Factorial Calculator**
**app.py**
```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial(n - 1)

num = int(input("Enter a number: "))
print("Factorial:", factorial(num))
```
**Dockerfile**
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . /app
CMD ["python", "app.py"]
```
**Commands:**
```bash
docker build -t factorial-app .
docker run -it factorial-app
```

---

## **Experiment 4: Palindrome Checker**
**app.py**
```python
text = input("Enter a string: ")
if text == text[::-1]:
    print("Palindrome")
else:
    print("Not a palindrome")
```
**Dockerfile**
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . /app
CMD ["python", "app.py"]
```
**Commands:**
```bash
docker build -t palindrome-app .
docker run -it palindrome-app
```

---

## **Experiment 5: Prime Number Checker**
**app.py**
```python
num = int(input("Enter a number: "))
if num > 1:
    for i in range(2, int(num**0.5) + 1):
        if num % i == 0:
            print("Not Prime")
            break
    else:
        print("Prime Number")
else:
    print("Not Prime")
```
**Dockerfile**
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . /app
CMD ["python", "app.py"]
```
**Commands:**
```bash
docker build -t prime-app .
docker run -it prime-app
```

---

## **Experiment 6: Fibonacci Series Generator**
**app.py**
```python
n = int(input("Enter number of terms: "))
a, b = 0, 1
print("Fibonacci Series:")
for i in range(n):
    print(a, end=" ")
    a, b = b, a + b
print()
```
**Dockerfile**
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . /app
CMD ["python", "app.py"]
```
**Commands:**
```bash
docker build -t fibonacci-app .
docker run -it fibonacci-app
```

---

## **Final Command Summary**
```bash
docker build -t hello-docker .
docker build -t arithmetic-calculator .
docker build -t factorial-app .
docker build -t palindrome-app .
docker build -t prime-app .
docker build -t fibonacci-app .

docker run hello-docker
docker run -it arithmetic-calculator
docker run -it factorial-app
docker run -it palindrome-app
docker run -it prime-app
docker run -it fibonacci-app
```
