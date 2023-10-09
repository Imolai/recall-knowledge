# TL;DR Python

## Python Basics

### Variables & Data Types


```python
name = "Gabor"
age = 42
is_student = False
print(name, age, is_student)
```

    Gabor 42 False


### List, Tuple, Set & Dictionary


```python
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)
my_set = {1, 2, 3}
my_dict = {"name": "Gabor", "age": 42}
print(my_list, my_tuple, my_set, my_dict)
```

    [1, 2, 3] (1, 2, 3) {1, 2, 3} {'name': 'Gabor', 'age': 42}


### Conditionals & Loops


```python
print(age)
if age > 18:
    print("Adult")
elif age < 13:
    print("Child")
else:
    print("Teenager")

print(list(range(5)))
for i in range(5):
    print(i)

while age < 49:
    age += 1
    print(age)

print(age)
```

    42
    Adult
    [0, 1, 2, 3, 4]
    0
    1
    2
    3
    4
    43
    44
    45
    46
    47
    48
    49
    49


### Functions


```python
def greet(name="Default"):
    return f"Hello, {name}"


print(greet())
print(greet("World"))
```

    Hello, Default
    Hello, World


### List Comprehension


```python
squares = [x * x for x in range(5)]
print(squares)

print(
    """
Equivalent imperative code:
squares = []
for x in range(5):
    squares.append(x * x)
print(squares)
"""
)
```

    [0, 1, 4, 9, 16]
    
    Equivalent imperative code:
    squares = []
    for x in range(5):
        squares.append(x * x)
    print(squares)
    


## Intermediate Python

### Classes & OOP


```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def intro(self):
        return f"Hello, my name is {self.name}."

    def old(self):
        return f"I am {self.age} years old."


gabor = Person("Gabor", 42)
print(gabor.intro())
print(gabor.old())
```

    Hello, my name is Gabor.
    I am 42 years old.


### Exceptions


```python
try:
    1 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
```

    Cannot divide by zero!


### Modules & Packages


```python
# import entire module
import math  # can throw ModuleNotFoundError

sqrt_4 = math.sqrt(4)

# import specific function
from math import sqrt  # can throw ImportError
```

### File Handling


```python
with open("file.txt", "w") as file:
    print("Hello Files!\n", file=file)

with open("file.txt", "r") as file:
    content = file.read()

print(f"'{content}'")
```

    'Hello Files!
    
    '


## Advanced Python

### Generators


```python
def my_gen(n):
    for i in range(n):
        yield i*i

gen = my_gen(5)

try:
    print(next(gen))
    print(next(gen))
    print(next(gen))
    print(next(gen))
    print(next(gen))
    print(next(gen))
except StopIteration:
    print("Iteration finished.")

gen = my_gen(5)
for g in gen:
    print(g)
```

    0
    1
    4
    9
    16
    Iteration finished.
    0
    1
    4
    9
    16



```python

```
