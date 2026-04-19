---
title: Untitled
date: 2026-04-19
author: Your Name
cell_count: 8
score: 5
---

```python
#type (to convert correct data type)
import argparse, sys

sys.argv = ["app.py", "--age", "21"]

parser = argparse.ArgumentParser()
parser.add_argument("--age", type=int)

args = parser.parse_args()
print(args.age, type(args.age))
```

    21 <class 'int'>
    


```python
#default(to set value if user does not give input)
import argparse, sys
sys.argv = ["app.py"]
parser = argparse.ArgumentParser()
parser.add_argument("--city", default="Chennai")
args = parser.parse_args()
print(args.city)
```

    Chennai
    


```python
#required (to make argument compulsory)

import argparse, sys

sys.argv = ["app.py", "--name", "Narmatha"]

parser = argparse.ArgumentParser()
parser.add_argument("--name", required=True)

args = parser.parse_args()
print(args.name)   # Narmatha
```

    Narmatha
    


```python
# help (to show description to user)
import argparse, sys
sys.argv = ["app.py", "--help"]
parser = argparse.ArgumentParser()
parser.add_argument("--name", help="Enter your name")
try:
    parser.parse_args()
except SystemExit:
    pass
```

    usage: app.py [-h] [--name NAME]
    
    options:
      -h, --help   show this help message and exit
      --name NAME  Enter your name
    


```python
#choices (to restrict input values)
import argparse, sys
sys.argv = ["app.py", "--role", "admin"]
parser = argparse.ArgumentParser()
parser.add_argument("--role", choices=["admin", "user"])
args = parser.parse_args()
print(args.role)   # admin
```

    admin
    


```python
# (to take multiple values)
import argparse, sys
sys.argv = ["app.py", "--nums", "1", "2", "3"]

parser = argparse.ArgumentParser()
parser.add_argument("--nums", nargs="+", type=int)
args = parser.parse_args()
print(args.nums)   # [1, 2, 3]
```

    [1, 2, 3]
    


```python
#const (to assign fixed value when no value is given)

import argparse, sys
sys.argv = ["app.py", "--mode"]
parser = argparse.ArgumentParser()
parser.add_argument("--mode", nargs="?", const="auto")

args = parser.parse_args()
print(args.mode)   # auto
```

    auto
    


```python












```


---
**Score: 5**