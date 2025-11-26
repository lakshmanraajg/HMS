# 📚 ZYLYTY Library App – REST API (Python + FastAPI + MySQL 8)

A complete backend system for user management, book cataloging, and borrowing operations.  
This project implements **secure API endpoints**, admin-only operations, session-based authentication, and full CRUD logic for books and borrowing.

The application is fully containerized using Docker and automatically initializes its database schema on startup.

---

# 🚀 Features

### 👤 **User System**
- Register new users  
- Secure password hashing (bcrypt + passlib)  
- Email encryption and hashing  
- Login + session cookies  
- SQL-injection prevention  
- Data validation  

### 📚 **Book Management (Admin Only)**
- Add one or multiple books  
- Update book details  
- Delete books  
- List books with pagination  
- Protection against repeated ISBN  
- Track `added_at` and `updated_at` timestamps  

### 📖 **Borrowing System (Users Only)**
- Borrow up to 5 books  
- Prevent borrowing already borrowed books  
- Return borrowed books  
- Track borrow and return timestamps  
- List all currently and previously borrowed books  

---

# 🛠 Technology Stack

| Layer | Technology |
|------|------------|
| Backend | FastAPI (Python) |
| ORM | SQLAlchemy 2 |
| Database | MySQL 8 |
| Security | bcrypt, passlib, session cookies |
| Validation | Pydantic |
| Containerization | Docker |

---

# ⚙️ Environment Variables

The evaluator (or you) must provide these:

| Variable | Description |
|---------|-------------|
| `ADMIN_API_KEY` | API key required for admin endpoints |
| `API_LISTENING_PORT` | Port where FastAPI will listen |
| `DB_HOST` | MySQL hostname |
| `DB_PORT` | MySQL port (default 3306) |
| `DB_NAME` | Database name |
| `DB_USERNAME` | Database user |
| `DB_PASSWORD` | Database password |

---

# ▶️ Running Locally (Without Docker)

### 1. Create virtual environment
python -m venv venv
venv\Scripts\activate.bat

### 2. Install dependencies
pip install -r requirements.txt

### 3. Export environment variables
`open cmd`
set ADMIN_API_KEY=anyname
set API_LISTENING_PORT=8000
set DB_HOST=localhost
set DB_PORT=3306
set DB_NAME=library
set DB_USERNAME="user name that u created(mysql)"
set DB_PASSWORD="password"     (without quotes)

### 4. Run server
`same cmd`
python -m app.main

### 5. Open Swagger UI
👉 http://localhost:8000/docs
`in browser`
---

# 🧪 Testing Flow (Recommended)
POST /user/register
POST /user/login → session cookie set
Authorize as admin → add books
GET /books
POST /borrow
GET /borrowed
DELETE /return/{isbn}
DELETE /books/{isbn}

---

# Common Errors & Fixes
Error	Meaning	Fix
401 - Missing admin API key	You didn't send Bearer token - Use Swagger "Authorize"
401 - Missing session cookie	User not logged in - Login first
400 - Weak password	Password not strong - Use strong password
400 - Duplicate ISBN	Book already exists - Use unique ISBN
