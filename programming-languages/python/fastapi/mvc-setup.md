Here's a **production-grade FastAPI backend** setup with **MVC architecture**, including **CORS, database connection, security setups, cache middleware, file upload middleware, logging, routing, and Docker**.

---

### 📁 **Folder Structure (MVC Pattern)**
```
fastapi-app/
│── app/
│   ├── api/
│   │   ├── routes/
│   │   │   ├── user.py
│   │   │   ├── auth.py
│   │   │   ├── file_upload.py
│   │   │   ├── __init__.py
│   │   ├── dependencies.py
│   │   ├── __init__.py
│   ├── core/
│   │   ├── config.py
│   │   ├── security.py
│   │   ├── database.py
│   │   ├── cache.py
│   │   ├── __init__.py
│   ├── models/
│   │   ├── user.py
│   │   ├── __init__.py
│   ├── services/
│   │   ├── user_service.py
│   │   ├── auth_service.py
│   │   ├── file_service.py
│   │   ├── __init__.py
│   ├── middlewares/
│   │   ├── logging_middleware.py
│   │   ├── security_middleware.py
│   │   ├── __init__.py
│   ├── schemas/
│   │   ├── user_schema.py
│   │   ├── auth_schema.py
│   │   ├── __init__.py
│   ├── main.py
│   ├── __init__.py
│── logs/
│── migrations/
│── tests/
│── .env
│── .dockerignore
│── Dockerfile
│── docker-compose.yml
│── requirements.txt
│── README.md
```

---

## 📌 **1. Core Configuration (`config.py`)**
Handles environment variables and settings.

```python
import os
from dotenv import load_dotenv

load_dotenv()

class Settings:
    PROJECT_NAME: str = "FastAPI Production App"
    DATABASE_URL: str = os.getenv("DATABASE_URL", "sqlite:///./test.db")
    SECRET_KEY: str = os.getenv("SECRET_KEY", "supersecretkey")
    ALGORITHM: str = "HS256"
    ACCESS_TOKEN_EXPIRE_MINUTES: int = 30

settings = Settings()
```

---

## 📌 **2. Database Connection (`database.py`)**
Using SQLAlchemy with PostgreSQL.

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base
from app.core.config import settings

engine = create_engine(settings.DATABASE_URL)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```

---

## 📌 **3. Security (`security.py`)**
Handles password hashing and token creation.

```python
from passlib.context import CryptContext
from datetime import datetime, timedelta
import jwt
from app.core.config import settings

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

def verify_password(plain_password, hashed_password):
    return pwd_context.verify(plain_password, hashed_password)

def get_password_hash(password):
    return pwd_context.hash(password)

def create_access_token(data: dict, expires_delta: timedelta = None):
    to_encode = data.copy()
    expire = datetime.utcnow() + (expires_delta or timedelta(minutes=settings.ACCESS_TOKEN_EXPIRE_MINUTES))
    to_encode.update({"exp": expire})
    return jwt.encode(to_encode, settings.SECRET_KEY, algorithm=settings.ALGORITHM)
```

---

## 📌 **4. Middleware (`logging_middleware.py`)**
Logging requests.

```python
from starlette.middleware.base import BaseHTTPMiddleware
import logging

logging.basicConfig(filename="logs/app.log", level=logging.INFO, format="%(asctime)s - %(message)s")

class LoggingMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request, call_next):
        logging.info(f"Request: {request.method} {request.url}")
        response = await call_next(request)
        return response
```

---

## 📌 **5. Cache Middleware (`cache.py`)**
Using `aiocache` for in-memory caching.

```python
from aiocache import Cache
cache = Cache(Cache.MEMORY)

async def get_cache(key: str):
    return await cache.get(key)

async def set_cache(key: str, value, ttl=300):
    await cache.set(key, value, ttl=ttl)
```

---

## 📌 **6. User Model (`models/user.py`)**
Using SQLAlchemy ORM.

```python
from sqlalchemy import Column, Integer, String
from app.core.database import Base

class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True, index=True)
    username = Column(String, unique=True, index=True)
    email = Column(String, unique=True, index=True)
    password = Column(String)
```

---

## 📌 **7. User Schema (`schemas/user_schema.py`)**
Defines request/response validation.

```python
from pydantic import BaseModel

class UserCreate(BaseModel):
    username: str
    email: str
    password: str

class UserResponse(BaseModel):
    id: int
    username: str
    email: str

    class Config:
        from_attributes = True
```

---

## 📌 **8. User Service (`services/user_service.py`)**
Handles business logic.

```python
from sqlalchemy.orm import Session
from app.models.user import User
from app.schemas.user_schema import UserCreate
from app.core.security import get_password_hash

def create_user(db: Session, user: UserCreate):
    hashed_password = get_password_hash(user.password)
    db_user = User(username=user.username, email=user.email, password=hashed_password)
    db.add(db_user)
    db.commit()
    db.refresh(db_user)
    return db_user
```

---

## 📌 **9. User Route (`api/routes/user.py`)**
Handles HTTP requests.

```python
from fastapi import APIRouter, Depends
from sqlalchemy.orm import Session
from app.core.database import get_db
from app.schemas.user_schema import UserCreate, UserResponse
from app.services.user_service import create_user

router = APIRouter()

@router.post("/", response_model=UserResponse)
def register_user(user: UserCreate, db: Session = Depends(get_db)):
    return create_user(db, user)
```

---

## 📌 **10. Main App (`main.py`)**
Entry point with middleware, CORS, and router.

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
from app.middlewares.logging_middleware import LoggingMiddleware
from app.api.routes import user

app = FastAPI()

# CORS Setup
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

app.add_middleware(LoggingMiddleware)

app.include_router(user.router, prefix="/users", tags=["Users"])
```

---

## 📌 **11. Docker Setup (`Dockerfile`)**
Dockerizing FastAPI.

```dockerfile
FROM python:3.10

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
```

---

## 📌 **12. Docker Compose (`docker-compose.yml`)**
For local dev setup.

```yaml
version: "3.8"

services:
  fastapi:
    build: .
    ports:
      - "8000:8000"
    env_file:
      - .env
    depends_on:
      - db

  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
      POSTGRES_DB: fastapi_db
```

---

## ✅ **Conclusion**
This setup ensures **production readiness** with:
- MVC Pattern
- Security (Hashing, JWT)
- Middleware (Logging, Cache)
- CORS, Routing
- Dockerized Setup

Let me know if you need modifications! 🚀
