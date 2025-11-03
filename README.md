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

[1](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/14006378/384ad09c-c986-4d99-9972-feaf1b2c51c5/containerzation-Lab-Manual-1-to-6-expts-.docx.pdf)
