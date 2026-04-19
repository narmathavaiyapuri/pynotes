---
title: Day4-Challenge
date: 2026-04-20
author: Your Name
cell_count: 9
score: 5
---

```python
!pip install pymongo python-dotenv certifi
```

    Requirement already satisfied: pymongo in C:\Users\Narmatha v\miniconda3\Lib\site-packages (4.16.0)
    Requirement already satisfied: python-dotenv in C:\Users\Narmatha v\miniconda3\Lib\site-packages (1.2.1)
    Requirement already satisfied: certifi in C:\Users\Narmatha v\miniconda3\Lib\site-packages (2026.1.4)
    Requirement already satisfied: dnspython<3.0.0,>=2.6.1 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from pymongo) (2.8.0)
    


```python
from pymongo import MongoClient
import certifi

MONGO_URI = "mongodb+srv://narmathavaiyapuri0121_db_user:HD4qb8609vqPEQFl@cluster01.28zme1j.mongodb.net/ai_pipeline?retryWrites=true&w=majority"

client = MongoClient(MONGO_URI, tls=True, tlsCAFile=certifi.where())

client.admin.command("ping")
print("MongoDB Connected ")

```

    MongoDB Connected 
    


```python
db = client["ai_pipeline"]
collection = db["ai_outputs"]

print("Database & Collection Ready ")
```

    Database & Collection Ready 
    


```python
from datetime import datetime, UTC

data = {
    "prompt": "What is AI?",
    "response": "AI is intelligence demonstrated by machines.",
    "timestamp": datetime.now(UTC)
}

result = collection.insert_one(data)
print("Inserted ID:", result.inserted_id)
```

    Inserted ID: 69e13afdf9cd65a9ab6bc59d
    


```python
for doc in collection.find():
    print(doc)
```

    {'_id': ObjectId('69e1384acc8b63ed9022157e'), 'prompt': 'What is AI?', 'response': 'AI is intelligence demonstrated by machines.', 'timestamp': datetime.datetime(2026, 4, 16, 19, 28, 10, 288000)}
    {'_id': ObjectId('69e1389cfae6442ebef350de'), 'prompt': 'What is AI?', 'response': 'AI is intelligence demonstrated by machines.', 'timestamp': datetime.datetime(2026, 4, 16, 19, 29, 32, 628000)}
    {'_id': ObjectId('69e1396a06d90e86a2f4f544'), 'prompt': 'What is AI?', 'response': 'AI is intelligence demonstrated by machines.', 'timestamp': datetime.datetime(2026, 4, 16, 19, 32, 58, 102000)}
    {'_id': ObjectId('69e13afdf9cd65a9ab6bc59d'), 'prompt': 'What is AI?', 'response': 'AI is intelligence demonstrated by machines.', 'timestamp': datetime.datetime(2026, 4, 16, 19, 39, 41, 400000)}
    


```python
result = collection.find_one({"prompt": "What is AI?"})
print(result)
```

    {'_id': ObjectId('69e1384acc8b63ed9022157e'), 'prompt': 'What is AI?', 'response': 'AI is intelligence demonstrated by machines.', 'timestamp': datetime.datetime(2026, 4, 16, 19, 28, 10, 288000)}
    


```python
results = collection.find({"prompt": "What is AI?"})

for r in results:
    print(r)
```

    {'_id': ObjectId('69e1384acc8b63ed9022157e'), 'prompt': 'What is AI?', 'response': 'AI is intelligence demonstrated by machines.', 'timestamp': datetime.datetime(2026, 4, 16, 19, 28, 10, 288000)}
    {'_id': ObjectId('69e1389cfae6442ebef350de'), 'prompt': 'What is AI?', 'response': 'AI is intelligence demonstrated by machines.', 'timestamp': datetime.datetime(2026, 4, 16, 19, 29, 32, 628000)}
    {'_id': ObjectId('69e1396a06d90e86a2f4f544'), 'prompt': 'What is AI?', 'response': 'AI is intelligence demonstrated by machines.', 'timestamp': datetime.datetime(2026, 4, 16, 19, 32, 58, 102000)}
    {'_id': ObjectId('69e13afdf9cd65a9ab6bc59d'), 'prompt': 'What is AI?', 'response': 'AI is intelligence demonstrated by machines.', 'timestamp': datetime.datetime(2026, 4, 16, 19, 39, 41, 400000)}
    


```python
print("Day 4 MongoDB Task Completed ")
```

    Day 4 MongoDB Task Completed 
    


```python

```


---
**Score: 5**