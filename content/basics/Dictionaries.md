---
title: Dictionaries
date: 2026-04-20
author: Your Name
cell_count: 4
score: 0
---

```python
# Add and update values
user = {"name": "Narmatha", "age": 21}

user["age"] = 22
user["city"] = "Chennai"

print(user)
```

    {'name': 'Narmatha', 'age': 22, 'city': 'Chennai'}
    


```python
# Remove element
data = {"a": 10, "b": 20, "c": 30}

data.pop("b")

print(data)
```

    {'a': 10, 'c': 30}
    


```python
# Loop through dictionary
marks = {"math": 80, "science": 90}

for subject, mark in marks.items():
    print(subject, mark)
```

    math 80
    science 90
    


```python

```


---
**Score: 0**