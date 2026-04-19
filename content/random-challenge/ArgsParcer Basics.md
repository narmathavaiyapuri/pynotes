---
title: Argsparcer Basics
date: 2026-04-20
author: Your Name
cell_count: 11
score: 10
---

```python
#Take user name
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--name")
args = parser.parse_args(["--name", "Alice"])
print("Hello", args.name)
```

    Hello Alice
    


```python
#Add two numbers
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--a", type=int)
parser.add_argument("--b", type=int)
args = parser.parse_args(["--a", "2", "--b", "3"])
print(args.a + args.b)
```

    5
    


```python
#Check even or odd
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--num", type=int)
args = parser.parse_args(["--num", "4"])

if args.num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

    Even
    


```python
#Loop using input
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--n", type=int)
args = parser.parse_args(["--n", "3"])

for i in range(args.n):
    print(i)
```

    0
    1
    2
    


```python
#Default value
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--city", default="Chennai")
args = parser.parse_args([])
print(args.city)
```

    Chennai
    


```python
#Boolean flag
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--debug", action="store_true")
args = parser.parse_args(["--debug"])

if args.debug:
    print("Debug ON")
```

    Debug ON
    


```python
#String length
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--text")
args = parser.parse_args(["--text", "hello"])
print(len(args.text))
```

    5
    


```python
#List input
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--nums", nargs=3)
args = parser.parse_args(["--nums", "1", "2", "3"])
print(args.nums)
```

    ['1', '2', '3']
    


```python
#Required input
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--email", required=True)
args = parser.parse_args(["--email", "a@mail.com"])
print(args.email)
```

    a@mail.com
    


```python
#Choice input
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--mode", choices=["read", "write"])
args = parser.parse_args(["--mode", "read"])
print(args.mode)
```

    read
    


```python

```


---
**Score: 10**