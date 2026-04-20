---
title: List Comprehension
date: 2026-04-21
author: Your Name
cell_count: 4
score: 0
---

```python
# Basic list comprehension
nums = [1, 2, 3, 4]

result = [x * 2 for x in nums]

print(result)
```

    [2, 4, 6, 8]
    


```python
# With condition
nums = [1, 2, 3, 4, 5]

result = [x for x in nums if x % 2 == 0]

print(result)
```

    [2, 4]
    


```python
# String list comprehension
words = ["hi", "hello", "python"]

result = [w.upper() for w in words]

print(result)
```

    ['HI', 'HELLO', 'PYTHON']
    


```python

```


---
**Score: 0**