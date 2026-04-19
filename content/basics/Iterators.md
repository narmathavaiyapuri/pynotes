---
title: Iterators
date: 2026-04-19
author: Your Name
cell_count: 4
score: 0
---

```python
# Basic iterator
nums = [1, 2, 3]

it = iter(nums)

print(next(it))
print(next(it))
print(next(it))
```

    1
    2
    3
    


```python
# Loop using iterator
data = [10, 20, 30]

it = iter(data)

for val in it:
    print(val)
```

    10
    20
    30
    


```python
# Custom iterator
class Count:
    def __init__(self, max):
        self.max = max
        self.current = 1

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= self.max:
            val = self.current
            self.current += 1
            return val
        else:
            raise StopIteration

c = Count(5)

for num in c:
    print(num)
```

    1
    2
    3
    4
    5
    


```python

```


---
**Score: 0**