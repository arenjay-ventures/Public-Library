---
layout: default
title: Python Cheatsheet
parent: Tools & Technology
grand_parent: References
nav_order: 9
---

# Python Cheatsheet

## **What is Python?**

Python is a high-level, interpreted programming language known for its simplicity and readability. It's essential for:
- **Data Science**: Pandas, NumPy, Matplotlib, Scikit-learn
- **Web Development**: Django, Flask, FastAPI
- **Automation**: Scripts, DevOps, system administration
- **Machine Learning**: TensorFlow, PyTorch, Keras
- **Career Growth**: One of the most in-demand programming languages

## **Installation & Setup**

### **Install Python**
```bash
# Download from python.org or use package manager
# Windows: Download installer from python.org
# macOS: brew install python
# Linux: sudo apt install python3 python3-pip

# Verify installation
python --version
python3 --version
pip --version
```

### **Virtual Environments**
```bash
# Create virtual environment
python -m venv myenv
python3 -m venv myenv

# Activate (Windows)
myenv\Scripts\activate

# Activate (Linux/macOS)
source myenv/bin/activate

# Deactivate
deactivate

# Install packages in virtual environment
pip install package_name
```

### **Package Management**
```bash
# Install packages
pip install package_name
pip install -r requirements.txt

# List installed packages
pip list
pip freeze > requirements.txt

# Upgrade packages
pip install --upgrade package_name
pip install -U package_name
```

## **Basic Syntax**

### **Variables & Data Types**
```python
# Variables
name = "John"
age = 25
height = 5.9
is_student = True

# Data types
print(type(name))        # <class 'str'>
print(type(age))         # <class 'int'>
print(type(height))      # <class 'float'>
print(type(is_student))  # <class 'bool'>

# Type conversion
age_str = str(age)
age_int = int("25")
height_float = float("5.9")
```

### **Strings**
```python
# String operations
name = "John Doe"
print(name.upper())           # JOHN DOE
print(name.lower())           # john doe
print(name.split())           # ['John', 'Doe']
print(name.replace("John", "Jane"))  # Jane Doe

# String formatting
name = "John"
age = 25
print(f"Hello, {name}! You are {age} years old.")
print("Hello, {}! You are {} years old.".format(name, age))
print("Hello, %s! You are %d years old." % (name, age))
```

### **Lists**
```python
# Create lists
fruits = ["apple", "banana", "orange"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]

# List operations
fruits.append("grape")         # Add item
fruits.insert(1, "mango")     # Insert at index
fruits.remove("banana")       # Remove item
fruits.pop()                  # Remove last item
fruits.sort()                # Sort list
fruits.reverse()             # Reverse list

# List comprehensions
squares = [x**2 for x in range(10)]
evens = [x for x in range(20) if x % 2 == 0]
```

### **Dictionaries**
```python
# Create dictionaries
person = {
    "name": "John",
    "age": 25,
    "city": "New York"
}

# Dictionary operations
person["email"] = "john@example.com"  # Add key-value
person.get("name")                    # Get value
person.keys()                        # Get all keys
person.values()                      # Get all values
person.items()                       # Get key-value pairs

# Dictionary comprehensions
squares = {x: x**2 for x in range(5)}
```

### **Tuples & Sets**
```python
# Tuples (immutable)
coordinates = (10, 20)
colors = ("red", "green", "blue")

# Sets (unique elements)
unique_numbers = {1, 2, 3, 4, 5}
set1 = {1, 2, 3}
set2 = {3, 4, 5}
union = set1 | set2              # Union
intersection = set1 & set2       # Intersection
difference = set1 - set2         # Difference
```

## **Control Flow**

### **Conditional Statements**
```python
# If-elif-else
age = 18
if age < 18:
    print("Minor")
elif age == 18:
    print("Just became adult")
else:
    print("Adult")

# Ternary operator
status = "adult" if age >= 18 else "minor"
```

### **Loops**
```python
# For loops
for i in range(5):
    print(i)

for fruit in ["apple", "banana", "orange"]:
    print(fruit)

# While loops
count = 0
while count < 5:
    print(count)
    count += 1

# Loop control
for i in range(10):
    if i == 3:
        continue    # Skip iteration
    if i == 7:
        break       # Exit loop
    print(i)
```

## **Functions**

### **Basic Functions**
```python
# Define function
def greet(name):
    return f"Hello, {name}!"

# Call function
message = greet("John")
print(message)

# Function with default parameters
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

# Function with multiple parameters
def add_numbers(a, b):
    return a + b

# Lambda functions
square = lambda x: x**2
print(square(5))  # 25
```

### **Advanced Functions**
```python
# Variable arguments
def sum_all(*args):
    return sum(args)

print(sum_all(1, 2, 3, 4))  # 10

# Keyword arguments
def create_person(**kwargs):
    return kwargs

person = create_person(name="John", age=25, city="NYC")

# Function annotations
def add(a: int, b: int) -> int:
    return a + b
```

## **Classes & Objects**

### **Basic Classes**
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def greet(self):
        return f"Hello, I'm {self.name}"
    
    def have_birthday(self):
        self.age += 1

# Create object
person = Person("John", 25)
print(person.greet())
person.have_birthday()
print(person.age)
```

### **Inheritance**
```python
class Student(Person):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id
    
    def study(self):
        return f"{self.name} is studying"

student = Student("Jane", 20, "12345")
print(student.greet())
print(student.study())
```

## **File Operations**

### **Reading Files**
```python
# Read entire file
with open("file.txt", "r") as file:
    content = file.read()
    print(content)

# Read line by line
with open("file.txt", "r") as file:
    for line in file:
        print(line.strip())

# Read all lines
with open("file.txt", "r") as file:
    lines = file.readlines()
```

### **Writing Files**
```python
# Write to file
with open("output.txt", "w") as file:
    file.write("Hello, World!")

# Append to file
with open("output.txt", "a") as file:
    file.write("\nNew line")

# Write multiple lines
lines = ["Line 1", "Line 2", "Line 3"]
with open("output.txt", "w") as file:
    file.writelines(lines)
```

## **Error Handling**

### **Try-Except**
```python
# Basic error handling
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
except Exception as e:
    print(f"An error occurred: {e}")
else:
    print("No errors occurred")
finally:
    print("This always runs")

# Custom exceptions
class CustomError(Exception):
    pass

def risky_function():
    raise CustomError("Something went wrong")

try:
    risky_function()
except CustomError as e:
    print(f"Custom error: {e}")
```

## **Popular Libraries**

### **Data Science Libraries**
```python
# NumPy for numerical computing
import numpy as np
arr = np.array([1, 2, 3, 4, 5])
print(arr.mean())  # 3.0

# Pandas for data manipulation
import pandas as pd
df = pd.DataFrame({
    'Name': ['John', 'Jane', 'Bob'],
    'Age': [25, 30, 35]
})
print(df.head())

# Matplotlib for plotting
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4], [1, 4, 2, 3])
plt.show()
```

### **Web Development**
```python
# Flask web framework
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, World!"

@app.route('/user/<name>')
def user(name):
    return f"Hello, {name}!"

if __name__ == '__main__':
    app.run(debug=True)
```

### **Automation**
```python
# OS operations
import os
print(os.getcwd())  # Current directory
os.mkdir("new_folder")  # Create directory
os.listdir(".")  # List files

# File operations
import shutil
shutil.copy("source.txt", "destination.txt")
shutil.move("old.txt", "new.txt")
```

## **Testing**

### **Unit Testing**
```python
import unittest

def add(a, b):
    return a + b

class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)
        self.assertEqual(add(0, 0), 0)

if __name__ == '__main__':
    unittest.main()
```

### **Running Tests**
```bash
# Run tests
python -m unittest test_file.py
python -m unittest discover  # Find and run all tests
```

## **Best Practices**

### **Code Style (PEP 8)**
```python
# Use meaningful variable names
user_name = "John"
user_age = 25

# Use snake_case for variables and functions
def calculate_average(numbers):
    return sum(numbers) / len(numbers)

# Use PascalCase for classes
class UserManager:
    pass

# Use UPPER_CASE for constants
MAX_USERS = 100
```

### **Documentation**
```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.
    
    Args:
        length (float): The length of the rectangle
        width (float): The width of the rectangle
    
    Returns:
        float: The area of the rectangle
    """
    return length * width
```

### **Virtual Environments**
```bash
# Always use virtual environments
python -m venv myproject
source myproject/bin/activate  # Linux/macOS
myproject\Scripts\activate     # Windows

# Create requirements.txt
pip freeze > requirements.txt

# Install from requirements.txt
pip install -r requirements.txt
```

## **Learning Resources**

### **Documentation**
- **[Python Official Docs](https://docs.python.org/3/)** - Official documentation
- **[PEP 8 Style Guide](https://pep8.org/)** - Code style guidelines
- **[Python Standard Library](https://docs.python.org/3/library/)** - Built-in modules

### **Tutorials**
- **[Python Tutorial](https://docs.python.org/3/tutorial/)** - Official tutorial
- **[Real Python](https://realpython.com/)** - Advanced Python tutorials
- **[Python.org Tutorial](https://docs.python.org/3/tutorial/)** - Comprehensive guide

### **Practice Platforms**
- **[LeetCode](https://leetcode.com/)** - Coding challenges
- **[HackerRank](https://www.hackerrank.com/)** - Programming challenges
- **[Codewars](https://www.codewars.com/)** - Coding kata
- **[Project Euler](https://projecteuler.net/)** - Mathematical problems

### **Popular Frameworks**
- **Django**: Full-featured web framework
- **Flask**: Lightweight web framework
- **FastAPI**: Modern API framework
- **Pandas**: Data manipulation
- **NumPy**: Numerical computing
- **Matplotlib**: Data visualization
- **Scikit-learn**: Machine learning

## **Common Patterns**

### **List Comprehensions**
```python
# Traditional way
squares = []
for x in range(10):
    squares.append(x**2)

# List comprehension
squares = [x**2 for x in range(10)]

# With condition
evens = [x for x in range(20) if x % 2 == 0]
```

### **Context Managers**
```python
# File operations
with open("file.txt", "r") as f:
    content = f.read()

# Custom context manager
class DatabaseConnection:
    def __enter__(self):
        print("Connecting to database")
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Closing database connection")

with DatabaseConnection() as db:
    print("Using database")
```

Remember: **Python is about readability and simplicity**. Start with basic syntax, practice with small projects, then move to frameworks and libraries. The Python community is vast and helpful - don't hesitate to ask questions and contribute to open source projects!