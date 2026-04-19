---
title: Class & Object
date: 2026-04-20
author: Your Name
cell_count: 4
score: 0
---

```python
# Basic class and object
class Person:
    def __init__(self, name):
        self.name = name

    def show(self):
        print("Name:", self.name)

p1 = Person("Narmatha")
p1.show()
```

    Name: Narmatha
    


```python
# Multiple attributes
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print(self.name, self.age)

s1 = Student("Narmatha", 21)
s1.display()
```

    Narmatha 21
    


```python
# Simple method logic
class Calculator:
    def add(self, a, b):
        return a + b

obj = Calculator()
print(obj.add(10, 5))
```

    15
    


```python

```


---
**Score: 0**