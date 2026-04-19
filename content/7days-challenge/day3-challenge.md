---
title: Day3-Challenge
date: 2026-04-19
author: Your Name
cell_count: 8
score: 5
---

```python
import sys
!"{sys.executable}" -m pip install pymongo
```

    Requirement already satisfied: pymongo in C:\Users\Narmatha v\AppData\Local\Programs\Python\Python313\Lib\site-packages (4.16.0)
    Requirement already satisfied: dnspython<3.0.0,>=2.6.1 in C:\Users\Narmatha v\AppData\Local\Programs\Python\Python313\Lib\site-packages (from pymongo) (2.8.0)
    


```python
import pymongo
print("MongoDB Ready ✅")
```

    MongoDB Ready ✅
    


```python
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017/")
db = client["genai_db"]
collection = db["chat_data"]

print("Connected ✅")
```

    Connected ✅
    


```python
import os
from dotenv import load_dotenv

load_dotenv(dotenv_path=r"C:\Users\Narmatha v\kact\pynotes\notebooks\.env", override=True)

print(os.getenv("MONGO_URI"))
```


```python
from pymongo import MongoClient
import os

client = MongoClient(os.getenv("MONGO_URI"))

db = client["test"]

print("Connected Successfully ✅")
```

    Connected Successfully ✅
    


```python
from datetime import datetime

collection = db["messages"]

collection.insert_one({
    "name": "Narmatha",
    "message": "Hello MongoDB 🚀",
    "date": datetime.now()
})

print("Inserted ✅")
```

    Inserted ✅
    


```python
for doc in collection.find():
    print(doc)
```

    {'_id': ObjectId('69e4acbabeed1ce2a6bbcfce'), 'name': 'Narmatha', 'message': 'Hello MongoDB 🚀', 'date': datetime.datetime(2026, 4, 19, 15, 51, 46, 285000)}
    


```python

```


---
**Score: 5**