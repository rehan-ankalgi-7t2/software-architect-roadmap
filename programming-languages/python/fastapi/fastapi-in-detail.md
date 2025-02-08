# **FastAPI: A Complete Guide** 🚀  

FastAPI is a **modern, fast, and highly efficient** web framework for building APIs with **Python 3.7+**. It is designed to deliver high performance comparable to **Node.js and Go**, thanks to **Starlette** (for ASGI capabilities) and **Pydantic** (for data validation).  

## **📌 Why FastAPI?**
✅ **Speed** - FastAPI is as fast as **Node.js & Go** (due to Starlette & async capabilities).  
✅ **Automatic Validation** - Uses **Pydantic** for request validation and serialization.  
✅ **Auto-Generated Docs** - Built-in **Swagger UI & ReDoc** for API documentation.  
✅ **Asynchronous Support** - Uses **async/await** for non-blocking operations.  
✅ **Type Hinting** - Uses **Python type hints** to define request and response models.  
✅ **Dependency Injection** - Easily manage dependencies like authentication, databases, etc.  
✅ **Security** - Supports **OAuth2, JWT, CORS, and API key authentication**.  

---

## **🛠️ Installation**
FastAPI requires Python 3.7+  
```bash
pip install fastapi uvicorn
```
- **`fastapi`** → Core framework  
- **`uvicorn`** → ASGI server for running FastAPI  

---

## **🔹 Basic FastAPI Example**
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def read_root():
    return {"message": "Hello, FastAPI!"}
```
### **Run the Server:**
```bash
uvicorn main:app --reload
```
### **Visit the API Docs:**
- **Swagger UI:** [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)  
- **ReDoc:** [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)  

---

## **🔹 Handling Request Parameters**
### **1️⃣ Path Parameters**
```python
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```
📌 **Type hinting (`int`) ensures automatic validation**.

### **2️⃣ Query Parameters**
```python
@app.get("/products/")
async def get_products(limit: int = 10, category: str = "all"):
    return {"limit": limit, "category": category}
```
🔹 `/products/?limit=5&category=books`

---

## **🔹 Request Body with Pydantic**
Use **Pydantic models** to validate request data.
```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int
    email: str

@app.post("/users/")
async def create_user(user: User):
    return {"message": f"User {user.name} created!", "user_data": user}
```
🔹 **Automatic validation for missing or incorrect fields.**

---

## **🔹 Dependency Injection**
FastAPI supports **dependency injection** for modular and testable code.
```python
from fastapi import Depends

def get_token():
    return "secure_token"

@app.get("/secure-data/")
async def secure_data(token: str = Depends(get_token)):
    return {"token": token}
```

---

## **🔹 Database Integration (MongoDB)**
Use **`motor`** for async MongoDB operations.
```python
from motor.motor_asyncio import AsyncIOMotorClient

MONGO_URI = "mongodb://localhost:27017"
client = AsyncIOMotorClient(MONGO_URI)
db = client.mydatabase

@app.get("/items/")
async def get_items():
    items = await db.items.find().to_list(100)
    return items
```

---

## **🔹 Authentication (JWT)**
FastAPI supports **OAuth2 with JWT tokens**.
```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/protected/")
async def protected(token: str = Depends(oauth2_scheme)):
    return {"message": "Access granted", "token": token}
```

---

## **🔹 Middleware**
FastAPI supports middleware for request processing.
```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Allow all origins
    allow_methods=["GET", "POST"],  # Allowed methods
    allow_headers=["*"],  # Allowed headers
)
```

---

## **🔹 Background Tasks**
Perform tasks asynchronously in the background.
```python
from fastapi import BackgroundTasks

def send_email(email: str):
    print(f"Sending email to {email}")

@app.post("/register/")
async def register(email: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(send_email, email)
    return {"message": "User registered"}
```

---

## **🔹 Deploy FastAPI with Docker**
Create a `Dockerfile`:
```dockerfile
FROM python:3.10

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### **Run with Docker**
```bash
docker build -t fastapi-app .
docker run -p 8000:8000 fastapi-app
```

---

## **🔹 Next Steps**
🔹 Integrate with **MongoDB, PostgreSQL, or Redis**  
🔹 Implement **JWT authentication**  
🔹 Deploy using **Docker & Kubernetes**  
🔹 Set up **CI/CD pipelines (GitHub Actions)**  

Would you like a **detailed guide on authentication, CI/CD, or production setup?** 🚀
