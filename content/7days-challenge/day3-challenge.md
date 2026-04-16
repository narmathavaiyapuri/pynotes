---
title: Day3-Challenge
date: 2026-04-16
author: Your Name
cell_count: 17
score: 15
---

```python
## SETUP / INSTALLATION
!pip install pymongo llama-cpp-python
```


```python
# IMPORTS
from llama_cpp import Llama
from pymongo import MongoClient
from datetime import datetime, timedelta
import json
```


```python
## LOAD GGUF MODEL (llama.cpp)
llm = Llama(
    model_path="models/your-model.gguf",
    n_ctx=2048,
    n_threads=4
)
```


```python
## TEXT GENERATION (temperature, top_p, max_tokens)
def generate_text(prompt):
    response = llm(
        prompt,
        max_tokens=200,
        temperature=0.7,
        top_p=0.9,
        stop=["</s>"]
    )
    return response["choices"][0]["text"]
```


```python
## MONGODB CONNECTION
client = MongoClient("mongodb://localhost:27017/")
db = client["ai_database"]
collection = db["memory"]
```


```python
# STORE MEMORY WITH DATE
def store_memory(user_input, ai_output):
    collection.insert_one({
        "user": user_input,
        "ai": ai_output,
        "date": datetime.utcnow()
    })
```


```python
## QUERY BY DATE RANGE
def get_memories(start_date, end_date):
    return list(collection.find({
        "date": {
            "$gte": start_date,
            "$lte": end_date
        }
    }))
```


```python
## UPDATE DOCUMENT (FIELD OPERATORS)
collection.update_one(
    {"user": "Hello"},
    {"$set": {"ai": "Hello! How can I help you?"}}
)
```


```python
# DELETE DOCUMENTS
collection.delete_one({"user": "Hello"})
```


```python
# DELETE DOCUMENTS
collection.delete_many({"user": {"$exists": True}})
```


```python
# RETRIEVE CONTEXT (RAG STYLE)
def retrieve_context(query):
    docs = collection.find({
        "user": {"$regex": query, "$options": "i"}
    })
    context = ""
    for d in docs:
        context += f"User: {d['user']}\nAI: {d['ai']}\n"
    return context
```


```python
# STATEFUL AI CHAT
def chat_with_memory(user_input):
    context = retrieve_context(user_input)
    prompt = f"""
You are a helpful AI.

Past memory:
{context}

User: {user_input}
AI:
"""
    output = generate_text(prompt)
    store_memory(user_input, output)
    return output
```


```python
# TOOL: CALCULATOR
def calculator_tool(expression):
    try:
        return str(eval(expression))
    except:
        return "Error"
```


```python
# BASIC AGENT (TOOL USAGE)
def agent(user_input):
    if "calculate" in user_input:
        expr = user_input.replace("calculate", "")
        return calculator_tool(expr)
    return chat_with_memory(user_input)
```


```python
# STRUCTURED OUTPUT (TEXT + JSON)
def structured_response(prompt):
    formatted_prompt = f"""
TEXT:
<your explanation>

JSON:
{{
    "summary": "...",
    "keywords": ["...", "..."]
}}

Question: {prompt}
"""
    return generate_text(formatted_prompt)
```


```python
# SMART AGENT (AUTO TOOL DECISION)
def smart_agent(user_input):
    decision_prompt = f"""
Tools:
- calculator

Input: {user_input}

Respond JSON:
{{
    "tool": "calculator" or "none",
    "input": "..."
}}
"""
    decision = generate_text(decision_prompt)

    try:
        decision_json = json.loads(decision)
        if decision_json["tool"] == "calculator":
            return calculator_tool(decision_json["input"])
    except:
        pass

    return chat_with_memory(user_input)
```


```python

```


---
**Score: 15**