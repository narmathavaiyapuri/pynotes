---
title: Lambda Functions
date: 2026-04-20
author: Your Name
cell_count: 4
score: 0
---

```python
# Basic lambda
add = lambda a, b: a + b

print(add(10, 5))
```

    15
    


```python
# Lambda with condition
check = lambda x: "Even" if x % 2 == 0 else "Odd"

print(check(7))
```

    Odd
    


```python
# Lambda with list
nums = [1, 2, 3, 4]

result = list(map(lambda x: x * 2, nums))

print(result)
```

    [2, 4, 6, 8]
    


```python

```


---
**Score: 0**