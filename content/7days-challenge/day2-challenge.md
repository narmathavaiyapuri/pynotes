---
title: Day2-Challenge
date: 2026-04-19
author: Your Name
cell_count: 2
score: 0
---

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from fastapi.middleware.cors import CORSMiddleware
from typing import List

app = FastAPI()

# Allow frontend
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# Model
class Item(BaseModel):
    name: str
    price: float

# In-memory DB
items: List[Item] = []

@app.get("/")
def home():
    return {"message": "API Running 🚀"}

@app.get("/items")
def get_items():
    return items

@app.post("/items")
def create_item(item: Item):
    items.append(item)
    return {"message": "Item added", "item": item}

@app.delete("/items/{index}")
def delete_item(index: int):
    if index >= len(items):
        raise HTTPException(status_code=404, detail="Item not found")
    return items.pop(index)
```


```python

```


---
**Score: 0**