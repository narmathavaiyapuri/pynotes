---
title: Day7-Challenge
date: 2026-04-21
author: Your Name
cell_count: 6
score: 5
---

```python
import os
from dotenv import load_dotenv

load_dotenv(dotenv_path=r"C:\Users\Narmatha v\kact\pynotes\notebooks\.env", override=True)

print(os.getenv("MONGO_URI"))

```


```python
from pymongo import MongoClient
import os

mongo_url = os.getenv("MONGO_URI")  
client = MongoClient(mongo_url)

db = client["ai_notes"]
collection = db["notes"]

for doc in collection.find():
    print(doc)

```

    {'_id': ObjectId('69e66a7ea4e634630431b812'), 'prompt': 'What is machine learning?', 'response': '', 'timestamp': datetime.datetime(2026, 4, 20, 18, 3, 42, 5000), 'session_id': 'my-session'}
    {'_id': ObjectId('69e66ae2a4e634630431b813'), 'prompt': 'What is machine learning?', 'response': 'How can it be used to improve healthcare outcomes?', 'timestamp': datetime.datetime(2026, 4, 20, 18, 5, 22, 949000), 'session_id': 'my-session'}
    {'_id': ObjectId('69e66bb4a4e634630431b814'), 'prompt': '<|user|>\nWhat is machine learning?\n<|assistant|>\n', 'response': 'Machine learning is a field in artificial intelligence (AI) that involves using algorithms and machine learning techniques to teach computers to learn from data and make decisions without being explicitly programmed. It is a branch of AI that has significant applications across various domains, including healthcare, finance, marketing, and more. The techniques involved in machine learning can be broadly categorized into three main areas: supervised learning, unsupervised learning, and reinforcement learning.\nIn supervised learning, a model is trained on a set of labeled data. The model is then used to make predictions on new data that has not been seen before. Unsupervised learning involves analyzing unlabeled data to discover patterns, which can be used to create predictive models. Reinforcement learning is an area of machine learning that involves the use of reinforcement agents (such as agents in games or robotics) to learn through trial and error.\nMachine learning techniques like neural networks, random forests, decision trees, and support vector machines have become increasingly popular in various industries. They are used to identify patterns in data, predict outcomes, and make informed decisions.', 'timestamp': datetime.datetime(2026, 4, 20, 18, 8, 52, 433000), 'session_id': 'my-session'}
    


```python
for doc in collection.find():
    print(doc)
```

    {'_id': ObjectId('69e66a7ea4e634630431b812'), 'prompt': 'What is machine learning?', 'response': '', 'timestamp': datetime.datetime(2026, 4, 20, 18, 3, 42, 5000), 'session_id': 'my-session'}
    {'_id': ObjectId('69e66ae2a4e634630431b813'), 'prompt': 'What is machine learning?', 'response': 'How can it be used to improve healthcare outcomes?', 'timestamp': datetime.datetime(2026, 4, 20, 18, 5, 22, 949000), 'session_id': 'my-session'}
    {'_id': ObjectId('69e66bb4a4e634630431b814'), 'prompt': '<|user|>\nWhat is machine learning?\n<|assistant|>\n', 'response': 'Machine learning is a field in artificial intelligence (AI) that involves using algorithms and machine learning techniques to teach computers to learn from data and make decisions without being explicitly programmed. It is a branch of AI that has significant applications across various domains, including healthcare, finance, marketing, and more. The techniques involved in machine learning can be broadly categorized into three main areas: supervised learning, unsupervised learning, and reinforcement learning.\nIn supervised learning, a model is trained on a set of labeled data. The model is then used to make predictions on new data that has not been seen before. Unsupervised learning involves analyzing unlabeled data to discover patterns, which can be used to create predictive models. Reinforcement learning is an area of machine learning that involves the use of reinforcement agents (such as agents in games or robotics) to learn through trial and error.\nMachine learning techniques like neural networks, random forests, decision trees, and support vector machines have become increasingly popular in various industries. They are used to identify patterns in data, predict outcomes, and make informed decisions.', 'timestamp': datetime.datetime(2026, 4, 20, 18, 8, 52, 433000), 'session_id': 'my-session'}
    


```python
data = list(collection.find())
print(data)
```

    [{'_id': ObjectId('69e66a7ea4e634630431b812'), 'prompt': 'What is machine learning?', 'response': '', 'timestamp': datetime.datetime(2026, 4, 20, 18, 3, 42, 5000), 'session_id': 'my-session'}, {'_id': ObjectId('69e66ae2a4e634630431b813'), 'prompt': 'What is machine learning?', 'response': 'How can it be used to improve healthcare outcomes?', 'timestamp': datetime.datetime(2026, 4, 20, 18, 5, 22, 949000), 'session_id': 'my-session'}, {'_id': ObjectId('69e66bb4a4e634630431b814'), 'prompt': '<|user|>\nWhat is machine learning?\n<|assistant|>\n', 'response': 'Machine learning is a field in artificial intelligence (AI) that involves using algorithms and machine learning techniques to teach computers to learn from data and make decisions without being explicitly programmed. It is a branch of AI that has significant applications across various domains, including healthcare, finance, marketing, and more. The techniques involved in machine learning can be broadly categorized into three main areas: supervised learning, unsupervised learning, and reinforcement learning.\nIn supervised learning, a model is trained on a set of labeled data. The model is then used to make predictions on new data that has not been seen before. Unsupervised learning involves analyzing unlabeled data to discover patterns, which can be used to create predictive models. Reinforcement learning is an area of machine learning that involves the use of reinforcement agents (such as agents in games or robotics) to learn through trial and error.\nMachine learning techniques like neural networks, random forests, decision trees, and support vector machines have become increasingly popular in various industries. They are used to identify patterns in data, predict outcomes, and make informed decisions.', 'timestamp': datetime.datetime(2026, 4, 20, 18, 8, 52, 433000), 'session_id': 'my-session'}]
    


```python
import pprint

for doc in collection.find():
    pprint.pprint(doc)
```

    {'_id': ObjectId('69e66a7ea4e634630431b812'),
     'prompt': 'What is machine learning?',
     'response': '',
     'session_id': 'my-session',
     'timestamp': datetime.datetime(2026, 4, 20, 18, 3, 42, 5000)}
    {'_id': ObjectId('69e66ae2a4e634630431b813'),
     'prompt': 'What is machine learning?',
     'response': 'How can it be used to improve healthcare outcomes?',
     'session_id': 'my-session',
     'timestamp': datetime.datetime(2026, 4, 20, 18, 5, 22, 949000)}
    {'_id': ObjectId('69e66bb4a4e634630431b814'),
     'prompt': '<|user|>\nWhat is machine learning?\n<|assistant|>\n',
     'response': 'Machine learning is a field in artificial intelligence (AI) that '
                 'involves using algorithms and machine learning techniques to '
                 'teach computers to learn from data and make decisions without '
                 'being explicitly programmed. It is a branch of AI that has '
                 'significant applications across various domains, including '
                 'healthcare, finance, marketing, and more. The techniques '
                 'involved in machine learning can be broadly categorized into '
                 'three main areas: supervised learning, unsupervised learning, '
                 'and reinforcement learning.\n'
                 'In supervised learning, a model is trained on a set of labeled '
                 'data. The model is then used to make predictions on new data '
                 'that has not been seen before. Unsupervised learning involves '
                 'analyzing unlabeled data to discover patterns, which can be used '
                 'to create predictive models. Reinforcement learning is an area '
                 'of machine learning that involves the use of reinforcement '
                 'agents (such as agents in games or robotics) to learn through '
                 'trial and error.\n'
                 'Machine learning techniques like neural networks, random '
                 'forests, decision trees, and support vector machines have become '
                 'increasingly popular in various industries. They are used to '
                 'identify patterns in data, predict outcomes, and make informed '
                 'decisions.',
     'session_id': 'my-session',
     'timestamp': datetime.datetime(2026, 4, 20, 18, 8, 52, 433000)}
    


```python

```


---
**Score: 5**