---
title: Day6-Challenge
date: 2026-04-20
author: Your Name
cell_count: 15
score: 15
---

```python
!python -m pip install llama-cpp-python fastapi uvicorn nest-asyncio pydantic
```

    Requirement already satisfied: llama-cpp-python in C:\Users\Narmatha v\miniconda3\Lib\site-packages (0.3.20)
    Requirement already satisfied: fastapi in C:\Users\Narmatha v\miniconda3\Lib\site-packages (0.136.0)
    Requirement already satisfied: uvicorn in C:\Users\Narmatha v\miniconda3\Lib\site-packages (0.44.0)
    Requirement already satisfied: nest-asyncio in C:\Users\Narmatha v\miniconda3\Lib\site-packages (1.6.0)
    Requirement already satisfied: pydantic in C:\Users\Narmatha v\miniconda3\Lib\site-packages (2.12.4)
    Requirement already satisfied: typing-extensions>=4.5.0 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from llama-cpp-python) (4.15.0)
    Requirement already satisfied: numpy>=1.20.0 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from llama-cpp-python) (2.4.4)
    Requirement already satisfied: diskcache>=5.6.1 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from llama-cpp-python) (5.6.3)
    Requirement already satisfied: jinja2>=2.11.3 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from llama-cpp-python) (3.1.6)
    Requirement already satisfied: starlette>=0.46.0 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from fastapi) (1.0.0)
    Requirement already satisfied: typing-inspection>=0.4.2 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from fastapi) (0.4.2)
    Requirement already satisfied: annotated-doc>=0.0.2 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from fastapi) (0.0.4)
    Requirement already satisfied: click>=7.0 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from uvicorn) (8.2.1)
    Requirement already satisfied: h11>=0.8 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from uvicorn) (0.16.0)
    Requirement already satisfied: annotated-types>=0.6.0 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from pydantic) (0.6.0)
    Requirement already satisfied: pydantic-core==2.41.5 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from pydantic) (2.41.5)
    Requirement already satisfied: colorama in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from click>=7.0->uvicorn) (0.4.6)
    Requirement already satisfied: MarkupSafe>=2.0 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from jinja2>=2.11.3->llama-cpp-python) (3.0.3)
    Requirement already satisfied: anyio<5,>=3.6.2 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from starlette>=0.46.0->fastapi) (4.10.0)
    Requirement already satisfied: idna>=2.8 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from anyio<5,>=3.6.2->starlette>=0.46.0->fastapi) (3.11)
    Requirement already satisfied: sniffio>=1.1 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from anyio<5,>=3.6.2->starlette>=0.46.0->fastapi) (1.3.1)
    


```python
import llama_cpp
import fastapi
import uvicorn
import nest_asyncio
import pydantic

print("llama-cpp-python:", llama_cpp.__version__)
print("fastapi:", fastapi.__version__)
print("uvicorn:", uvicorn.__version__)
print("pydantic:", pydantic.__version__)
print("\n All imports successful!")
```

    llama-cpp-python: 0.3.20
    fastapi: 0.116.1
    uvicorn: 0.35.0
    pydantic: 2.11.9
    
     All imports successful!
    


```python
import os

model_path = "./models/mistral-7b-instruct-v0.1.Q4_K_M.gguf"
print("Model found:", os.path.exists(model_path))
```

    Model found: False
    


```python
from contextlib import asynccontextmanager
from fastapi import FastAPI
from pydantic import BaseModel, Field
from llama_cpp import Llama
import uvicorn
import nest_asyncio
import threading

nest_asyncio.apply()

llm = None
print("All imports done.")
```

    All imports done.
    


```python
class PromptRequest(BaseModel):
    prompt: str
    max_tokens: int = Field(default=256, ge=1, le=2048)
    temperature: float = Field(default=0.7, ge=0.0, le=2.0)

class PromptResponse(BaseModel):
    prompt: str
    response: str
    tokens_used: int

print("Schemas ready.")
```

    Schemas ready.
    


```python
@asynccontextmanager
async def lifespan(app: FastAPI):
    global llm
    print("Loading model...")
    llm = Llama(
        model_path="./models/mistral-7b-instruct-v0.1.Q4_K_M.gguf",
        n_ctx=2048,
        n_threads=4,
        verbose=False,
    )
    print("Model loaded.")
    yield
    llm = None

app = FastAPI(title="Local LLM API", lifespan=lifespan)

@app.get("/health")
def health():
    return {"status": "ok", "model_loaded": llm is not None}

@app.post("/generate", response_model=PromptResponse)
def generate(req: PromptRequest):
    output = llm(
        req.prompt,
        max_tokens=req.max_tokens,
        temperature=req.temperature,
        stop=["</s>", "\n\n"],
    )
    text = output["choices"][0]["text"].strip()
    tokens = output["usage"]["total_tokens"]
    return PromptResponse(prompt=req.prompt, response=text, tokens_used=tokens)

print("App and endpoints defined.")
```

    App and endpoints defined.
    


```python
def run_server():
    uvicorn.run(app, host="0.0.0.0", port=8000)

thread = threading.Thread(target=run_server, daemon=True)
thread.start()

print("Server running at http://localhost:8000")
print("Swagger UI at  http://localhost:8000/docs")
```

    Server running at http://localhost:8000
    Swagger UI at  http://localhost:8000/docs
    

    INFO:     Started server process [23872]
    INFO:     Waiting for application startup.
    ERROR:    Traceback (most recent call last):
      File "C:\Users\Narmatha v\AppData\Local\Programs\Python\Python313\Lib\site-packages\starlette\routing.py", line 694, in lifespan
        async with self.lifespan_context(app) as maybe_state:
                   ~~~~~~~~~~~~~~~~~~~~~^^^^^
      File "C:\Users\Narmatha v\AppData\Local\Programs\Python\Python313\Lib\contextlib.py", line 214, in __aenter__
        return await anext(self.gen)
               ^^^^^^^^^^^^^^^^^^^^^
      File "C:\Users\Narmatha v\AppData\Local\Temp\ipykernel_23872\3219729982.py", line 5, in lifespan
        llm = Llama(
            model_path="./models/mistral-7b-instruct-v0.1.Q4_K_M.gguf",
        ...<2 lines>...
            verbose=False,
        )
      File "C:\Users\Narmatha v\AppData\Local\Programs\Python\Python313\Lib\site-packages\llama_cpp\llama.py", line 377, in __init__
        raise ValueError(f"Model path does not exist: {model_path}")
    ValueError: Model path does not exist: ./models/mistral-7b-instruct-v0.1.Q4_K_M.gguf
    
    ERROR:    Application startup failed. Exiting.
    

    Loading model...
    


```python
@asynccontextmanager
async def lifespan(app: FastAPI):
    global llm
    print("Loading model...")
    llm = Llama(
        model_path="C:/Users/Narmatha v/kact/tinyllama-1.1b-chat-v1.0.Q4_K_M.gguf",
        n_ctx=2048,
        n_threads=4,
        verbose=False,
    )
    print("Model loaded.")
    yield
    llm = None

app = FastAPI(title="Local LLM API", lifespan=lifespan)

@app.get("/health")
def health():
    return {"status": "ok", "model_loaded": llm is not None}

@app.post("/generate", response_model=PromptResponse)
def generate(req: PromptRequest):
    output = llm(
        req.prompt,
        max_tokens=req.max_tokens,
        temperature=req.temperature,
        stop=["</s>", "\n\n"],
    )
    text = output["choices"][0]["text"].strip()
    tokens = output["usage"]["total_tokens"]
    return PromptResponse(prompt=req.prompt, response=text, tokens_used=tokens)

print("App and endpoints defined.")
```

    App and endpoints defined.
    


```python
def run_server():
    uvicorn.run(app, host="0.0.0.0", port=8000)

thread = threading.Thread(target=run_server, daemon=True)
thread.start()

print("Server running at http://localhost:8000")
print("Swagger UI at  http://localhost:8000/docs")
```

    Server running at http://localhost:8000
    Swagger UI at  http://localhost:8000/docs
    

    INFO:     Started server process [23872]
    INFO:     Waiting for application startup.
    

    Loading model...
    

    INFO:     Application startup complete.
    INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
    

    Model loaded.
    INFO:     127.0.0.1:49253 - "GET / HTTP/1.1" 404 Not Found
    INFO:     127.0.0.1:49253 - "GET /favicon.ico HTTP/1.1" 404 Not Found
    INFO:     127.0.0.1:49253 - "GET /docs HTTP/1.1" 200 OK
    INFO:     127.0.0.1:49253 - "GET /openapi.json HTTP/1.1" 200 OK
    INFO:     127.0.0.1:49253 - "GET /docs HTTP/1.1" 200 OK
    INFO:     127.0.0.1:49253 - "GET /openapi.json HTTP/1.1" 200 OK
    INFO:     127.0.0.1:54036 - "GET /docs HTTP/1.1" 200 OK
    INFO:     127.0.0.1:54036 - "GET /openapi.json HTTP/1.1" 200 OK
    INFO:     127.0.0.1:52906 - "POST /generate HTTP/1.1" 200 OK
    


```python
import requests

res = requests.post("http://localhost:8000/generate", json={
    "prompt": "What is artificial intelligence?",
    "max_tokens": 80,
    "temperature": 0.5
})

print(res.json())
```

    INFO:     127.0.0.1:49679 - "POST /generate HTTP/1.1" 200 OK
    {'prompt': 'What is artificial intelligence?', 'response': 'How is it used in healthcare, and how is its role evolving?', 'tokens_used': 22}
    


```python
import subprocess

result = subprocess.run([
    "curl", "-X", "POST", "http://localhost:8000/generate",
    "-H", "Content-Type: application/json",
    "-d", '{"prompt": "Explain AI in one sentence.", "max_tokens": 60, "temperature": 0.5}'
], capture_output=True, text=True)

print(result.stdout)
```

    INFO:     127.0.0.1:50865 - "POST /generate HTTP/1.1" 200 OK
    {"prompt":"Explain AI in one sentence.","response":"AI is an artificial intelligence.\nAI is an artificial intelligence that is not created by humans.\nAI is an artificial intelligence that is created by humans.\nAI is a type of machine learning.\nAI is a type of machine learning that is not created by humans.\nAI is a","tokens_used":69}
    


```python
import requests

prompts = [
    "What is Python?",
    "What is an API?",
    "Explain machine learning briefly.",
]

for p in prompts:
    res = requests.post("http://localhost:8000/generate", json={
        "prompt": p,
        "max_tokens": 60,
        "temperature": 0.7
    })
    data = res.json()
    print(f"Q: {data['prompt']}")
    print(f"A: {data['response']}")
    print(f"Tokens used: {data['tokens_used']}")
    print("-" * 50)
```

    INFO:     127.0.0.1:58525 - "POST /generate HTTP/1.1" 200 OK
    Q: What is Python?
    A: 
    Tokens used: 7
    --------------------------------------------------
    INFO:     127.0.0.1:52126 - "POST /generate HTTP/1.1" 200 OK
    Q: What is an API?
    A: 
    Tokens used: 6
    --------------------------------------------------
    INFO:     127.0.0.1:52128 - "POST /generate HTTP/1.1" 200 OK
    Q: Explain machine learning briefly.
    A: 
    Tokens used: 7
    --------------------------------------------------
    


```python
import os
from dotenv import load_dotenv

load_dotenv(dotenv_path=r"C:\Users\Narmatha v\kact\pynotes\notebooks\.env", override=True)

MONGO_URI = os.getenv("MONGO_URI")

if MONGO_URI:
    print("✅ URI loaded successfully!")
    print("Preview:", MONGO_URI[:30], "...")
else:
    print("❌ MONGO_URI not found — .env file check பண்ணுங்க")
```


```python
from pymongo import MongoClient
import requests, datetime

client = MongoClient(MONGO_URI)
db = client["llm_db"]
collection = db["responses"]

# Connection test
client.server_info()
print("✅ MongoDB Atlas connected!")

# Save LLM responses
prompts = ["What is FastAPI?", "What is llama.cpp?"]

for p in prompts:
    res = requests.post("http://localhost:8000/generate", json={
        "prompt": p, "max_tokens": 80, "temperature": 0.5
    })
    data = res.json()
    collection.insert_one({
        "prompt": data["prompt"],
        "response": data["response"],
        "tokens_used": data["tokens_used"],
        "timestamp": datetime.datetime.now()
    })
    print(f"✅ Saved: {p}")

# Read back
print("\n--- Stored Responses ---")
for doc in collection.find():
    print(f"Q: {doc['prompt']}")
    print(f"A: {doc['response']}")
    print(f"Tokens: {doc['tokens_used']}")
    print("-" * 40)
```

    ✅ MongoDB Atlas connected!
    INFO:     127.0.0.1:51669 - "POST /generate HTTP/1.1" 200 OK
    ✅ Saved: What is FastAPI?
    INFO:     127.0.0.1:51671 - "POST /generate HTTP/1.1" 200 OK
    ✅ Saved: What is llama.cpp?
    
    --- Stored Responses ---
    Q: What is FastAPI?
    A: 
    Tokens: 6
    ----------------------------------------
    Q: What is llama.cpp?
    A: Can you provide me with a brief explanation of the purpose and structure of the file?
    Tokens: 25
    ----------------------------------------
    INFO:     127.0.0.1:55314 - "GET /docs HTTP/1.1" 200 OK
    INFO:     127.0.0.1:55314 - "GET /openapi.json HTTP/1.1" 200 OK
    INFO:     127.0.0.1:61333 - "POST /generate HTTP/1.1" 200 OK
    INFO:     127.0.0.1:63606 - "GET /docs HTTP/1.1" 200 OK
    INFO:     127.0.0.1:63606 - "GET /openapi.json HTTP/1.1" 200 OK
    


```python

```


---
**Score: 15**