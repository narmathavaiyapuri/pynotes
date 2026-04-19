---
title: Sets
date: 2026-04-19
author: Your Name
cell_count: 4
score: 0
---

```python
# Loop through tuple
nums = (5, 10, 15)

total = 0

for n in nums:
    total += n

print("Total:", total)
```

    Total: 30
    


```python
# Union and intersection
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)   # union
print(a & b)   # intersection
```

    {1, 2, 3, 4, 5}
    {3}
    


```python
# Difference and symmetric difference
x = {10, 20, 30}
y = {20, 40}

print(x - y)   # difference
print(x ^ y)   # symmetric difference
```

    {10, 30}
    {40, 10, 30}
    


```python

```


---
**Score: 0**