---
title: File Handling
date: 2026-04-21
author: Your Name
cell_count: 4
score: 0
---

```python
# Write to file
file = open("test.txt", "w")

file.write("Hello Narmatha")
file.close()
```


```python
# Read from file
file = open("test.txt", "r")

data = file.read()
print(data)

file.close()
```

    Hello Narmatha
    


```python
# Append to file
file = open("test.txt", "a")

file.write("\nNew Line Added")

file.close()
```


```python

```


---
**Score: 0**