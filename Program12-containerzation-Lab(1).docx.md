**Program-12: Temperature Converter (Celsius ↔ Fahrenheit) in Docker (OFFLINE)**  
**📌 Objective**

Create a simple Python program that converts temperature values, and run it fully inside a Docker container **without requiring internet**.

**Step 1: Create a folder**

mkdir TempConverter  
cd TempConverter

**Step 2: Create Python Program**

Create a file named **temp.py**:

def c\_to\_f(c):  
    return (c \* 9/5) \+ 32

def f\_to\_c(f):  
    return (f \- 32\) \* 5/9

if \_\_name\_\_ \== "\_\_main\_\_":  
    print("=== Temperature Converter (Docker Offline) \===")  
    print("1. Celsius to Fahrenheit")  
    print("2. Fahrenheit to Celsius")  
      
    choice \= input("Enter choice (1 or 2): ")

    if choice \== "1":  
        c \= float(input("Enter Celsius: "))  
        print("Fahrenheit \=", c\_to\_f(c))  
    elif choice \== "2":  
        f \= float(input("Enter Fahrenheit: "))  
        print("Celsius \=", f\_to\_c(f))  
    else:  
        print("Invalid choice\!")

This works fully offline and needs **no external libraries**.

**Step 3: Create Dockerfile**

Create a file **Dockerfile**:

FROM python:3.9-slim

WORKDIR /app

COPY temp.py .

CMD \["python", "temp.py"\]

**Step 4: Build Image (Offline)**

docker build \-t temp-converter .

✔️ Works offline because most labs already have  
python:3.9-slim image pre-pulled during earlier experiments.

**Step 5: Run Container**

docker run \-it temp-converter

**Expected Output**

\=== Temperature Converter (Docker Offline) \===  
1\. Celsius to Fahrenheit  
2\. Fahrenheit to Celsius  
Enter choice (1 or 2): 1  
Enter Celsius: 37  
Fahrenheit \= 98.6

or

Enter choice (1 or 2): 2  
Enter Fahrenheit: 100  
Celsius \= 37.7777

rit@rit:\~$ mkdir TempConverter

rit@rit:\~$ cd TempConverter

rit@rit:\~/TempConverter$ nano temp.py

rit@rit:\~/TempConverter$ vi Dockerfile

rit@rit:\~/TempConverter$ sudo docker build \-t temp-converter .

\[sudo\] password for rit: 

\[

rit@rit:\~/TempConverter$ sudo docker run \-it temp-converter

\=== Temperature Converter (Docker Offline) \===

1\. Celsius to Fahrenheit

2\. Fahrenheit to Celsius

Enter choice (1 or 2): 1

Enter Celsius: 37

Fahrenheit \= 98.6

rit@rit:\~/TempConverter$ 

