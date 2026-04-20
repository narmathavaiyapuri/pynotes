---
title: Argsparser Concepts
date: 2026-04-21
author: Your Name
cell_count: 8
score: 5
---

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--name")

args = parser.parse_args(args=[])

print("Name:", args.name)
```

    Name: None
    


```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("filename")

args = parser.parse_args(["data.txt"])

print("File:", args.filename)
```

    File: data.txt
    


```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--age", type=int)

args = parser.parse_args(["--age", "21"])

print("Age + 5 =", args.age + 5)
```

    Age + 5 = 26
    


```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--country", default="India")

args = parser.parse_args(args=[])

print("Country:", args.country)
```

    Country: India
    


```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--debug", action="store_true")

args = parser.parse_args(["--debug"])

if args.debug:
    print("Debug Mode ON")
else:
    print("Debug Mode OFF")
```

    Debug Mode ON
    


```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("--name")
parser.add_argument("--age", type=int)

args = parser.parse_args(["--name", "Raj", "--age", "20"])

print("Name:", args.name)
print("Age:", args.age)
```

    Name: Raj
    Age: 20
    


```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("--email", required=True)

args = parser.parse_args(["--email", "test@mail.com"])

print("Email:", args.email)
```

    Email: test@mail.com
    


```python

```


---
**Score: 5**