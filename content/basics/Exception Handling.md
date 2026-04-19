---
title: Exception Handling
date: 2026-04-20
author: Your Name
cell_count: 4
score: 0
---

```python
# Basic try-except
try:
    num = int("abc")
except:
    print("Error occurred")
```

    Error occurred
    


```python
# Specific exception
try:
    a = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
```

    Cannot divide by zero
    


```python
# finally block
try:
    x = int("100")
    print(x)
except:
    print("Error")
finally:
    print("Done execution")
```

    100
    Done execution
    


```python

```


---
**Score: 0**