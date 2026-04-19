---
title: Json Handling
date: 2026-04-20
author: Your Name
cell_count: 4
score: 0
---

```python
# Convert dict to JSON
import json

data = {"name": "Narmatha", "age": 21}

json_data = json.dumps(data)

print(json_data)
```

    {"name": "Narmatha", "age": 21}
    


```python
# Convert JSON to dict
import json

json_str = '{"name": "Narmatha", "age": 21}'

data = json.loads(json_str)

print(data["name"])
```

    Narmatha
    


```python
import json

try:
    with open("data.json", "r") as file:
        data = json.load(file)
        print(data)
except Exception as e:
    print("Error:", e)
```

    Error: [Errno 2] No such file or directory: 'data.json'
    


```python

```


---
**Score: 0**