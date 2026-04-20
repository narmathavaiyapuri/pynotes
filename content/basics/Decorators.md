---
title: Decorators
date: 2026-04-21
author: Your Name
cell_count: 4
score: 0
---

```python
# Basic decorator
def my_decorator(func):
    def wrapper():
        print("Before function")
        func()
        print("After function")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

    Before function
    Hello!
    After function
    


```python
# Decorator with arguments
def my_decorator(func):
    def wrapper(name):
        print("Welcome")
        func(name)
    return wrapper

@my_decorator
def greet(name):
    print("Hello", name)

greet("Narmatha")
```

    Welcome
    Hello Narmatha
    


```python
# Returning value
def my_decorator(func):
    def wrapper(a, b):
        result = func(a, b)
        return result * 2
    return wrapper

@my_decorator
def add(a, b):
    return a + b

print(add(5, 5))
```

    20
    


```python

```


---
**Score: 0**