---
title: Generators
date: 2026-04-20
author: Your Name
cell_count: 4
score: 0
---

```python
# Basic generator
def my_gen():
    yield 1
    yield 2
    yield 3

for val in my_gen():
    print(val)
```

    1
    2
    3
    


```python
# Generator with loop
def count(n):
    for i in range(n):
        yield i

for num in count(5):
    print(num)
```

    0
    1
    2
    3
    4
    


```python
# Using next()
def even_numbers():
    yield 2
    yield 4
    yield 6

g = even_numbers()

print(next(g))
print(next(g))
print(next(g))
```

    2
    4
    6
    


```python

```


---
**Score: 0**