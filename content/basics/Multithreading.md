---
title: Multithreading
date: 2026-04-21
author: Your Name
cell_count: 4
score: 0
---

```python
# Basic thread
import threading

def task():
    print("Task running")

t = threading.Thread(target=task)
t.start()
t.join()
```

    Task running
    


```python
# Multiple threads
import threading

def print_num(n):
    print("Number:", n)

threads = []

for i in range(3):
    t = threading.Thread(target=print_num, args=(i,))
    threads.append(t)
    t.start()

for t in threads:
    t.join()
```

    Number: 0
    Number: 1
    Number: 2
    


```python
# Thread with delay
import threading
import time

def task():
    for i in range(3):
        print("Running...")
        time.sleep(1)

t = threading.Thread(target=task)
t.start()
t.join()
```

    Running...
    Running...
    Running...
    


```python

```


---
**Score: 0**