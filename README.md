# Full Stack Tutorial: Python FastAPI + Next.js + React + PostgreSQL

A complete step-by-step guide to building a modern full-stack application with:
- **Backend**: Python (FastAPI)
- **Frontend**: React (Next.js with TypeScript)
- **Database**: PostgreSQL (local setup, no Docker)
- **Communication**: REST API between Python backend and Next.js server

## 🏗️ Project Structure

```
full-stack-python-nextjs-tutorial/
├── backend/                 # Python FastAPI backend
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py         # FastAPI application
│   │   ├── api/
│   │   │   ├── __init__.py
│   │   │   └── routes.py   # API endpoints
│   │   └── models.py       # Pydantic models
│   ├── requirements.txt    # Python dependencies
│   ├── .env.example       # Environment template
│   └── README.md          # Backend setup
│
├── frontend/               # Next.js + React project
│   ├── pages/
│   │   ├── api/
│   │   │   └── users.ts   # Proxy to FastAPI
│   │   ├── _app.tsx
│   │   ├── _document.tsx
│   │   └── index.tsx      # Home page
│   ├── styles/            # CSS files
│   ├── .env.local.example # Environment template
│   ├── package.json
│   ├── tsconfig.json
│   ├── next.config.js
│   └── README.md          # Frontend setup
│
└── README.md             # This file
```

## 🚀 Quick Start

### Prerequisites
- Python 3.9+
- Node.js 18+
- PostgreSQL (local installation)

### Step 1: Install PostgreSQL

**macOS:**
```bash
brew install postgresql@15
brew services start postgresql@15
```

**Windows:**
Download from: https://www.postgresql.org/download/windows/

**Linux (Ubuntu/Debian):**
```bash
sudo apt-get install postgresql postgresql-contrib
sudo service postgresql start
```

### Step 2: Create Database

```bash
psql -U postgres

# Inside psql:
CREATE DATABASE fullstack_db;
CREATE USER "user" WITH PASSWORD 'password';
GRANT ALL PRIVILEGES ON DATABASE fullstack_db TO "user";
\q
```

### Step 3: Setup Backend (Python FastAPI)

```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
```

Edit `backend/.env`:
```
DATABASE_URL=postgresql://user:password@localhost:5432/fullstack_db
FASTAPI_ENV=development
```

Start backend:
```bash
uvicorn app.main:app --reload --port 8000
```

Backend will be at: **http://localhost:8000**
API Docs: **http://localhost:8000/docs**

### Step 4: Setup Frontend (Next.js + React)

```bash
cd frontend
npm install
cp .env.local.example .env.local
npm run dev
```

Frontend will be at: **http://localhost:3000**

## 📊 Architecture

```
React Component (http://localhost:3000)
    ↓ (fetch('/api/users'))
Next.js API Route (pages/api/users.ts)
    ↓ (axios to http://localhost:8000)
Python FastAPI Backend
    ↓ (queries)
PostgreSQL Database (localhost:5432)
```

## 🔄 How Communication Works

### Example: Fetching Users

**Frontend (React):**
```typescript
const response = await fetch('/api/users')
const users = await response.json()
```

**Next.js API Route** (`pages/api/users.ts`):
```typescript
const response = await axios.get('http://localhost:8000/api/users')
res.status(200).json(response.data)
```

**FastAPI Backend** (`app/api/routes.py`):
```python
@router.get("/api/users")
async def get_users():
    return users_db
```

## 📚 API Endpoints

### Users
- `GET /api/users` - Get all users
- `GET /api/users/{id}` - Get user by ID
- `POST /api/users` - Create new user
- `PUT /api/users/{id}` - Update user
- `DELETE /api/users/{id}` - Delete user

### Posts
- `GET /api/posts` - Get all posts
- `GET /api/posts/{id}` - Get post by ID
- `GET /api/users/{id}/posts` - Get user's posts
- `POST /api/posts` - Create new post
- `PUT /api/posts/{id}` - Update post
- `DELETE /api/posts/{id}` - Delete post

## 🛠️ Development Workflow

### Running All Services

**Terminal 1 - FastAPI Backend:**
```bash
cd backend
source venv/bin/activate
uvicorn app.main:app --reload --port 8000
```

**Terminal 2 - Next.js Frontend:**
```bash
cd frontend
npm run dev
```

Now you have:
- Frontend: http://localhost:3000
- Backend: http://localhost:8000
- Backend Docs: http://localhost:8000/docs
- Database: localhost:5432

## 📖 Learning Path

### Beginner
1. Read this README
2. Setup PostgreSQL locally
3. Run backend and frontend
4. Make a GET request from React to FastAPI
5. View data in browser

### Intermediate
6. Add a new endpoint in FastAPI
7. Create a React form to POST data
8. Handle errors and loading states
9. Use TypeScript types

### Advanced
10. Add authentication (JWT)
11. Implement file uploads
12. Deploy to production
13. Add testing

## 🔍 Troubleshooting

### PostgreSQL Connection Error
```bash
# Test connection
psql -U user -d fullstack_db -h localhost
```

### Port 8000 or 3000 Already in Use
```bash
lsof -i :8000  # or :3000
kill -9 <PID>
```

### Python Virtual Environment Issues
```bash
cd backend
rm -rf venv
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Node Modules Issues
```bash
cd frontend
rm -rf node_modules package-lock.json
npm install
```

## 📝 Environment Variables

### Backend (.env)
```
DATABASE_URL=postgresql://user:password@localhost:5432/fullstack_db
FASTAPI_ENV=development
DEBUG=True
```

### Frontend (.env.local)
```
NEXT_PUBLIC_API_URL=http://localhost:8000
```

## 📚 Resources

- [FastAPI Docs](https://fastapi.tiangolo.com/)
- [Next.js Docs](https://nextjs.org/docs)
- [React Docs](https://react.dev)
- [PostgreSQL Docs](https://www.postgresql.org/docs/)
- [TypeScript Docs](https://www.typescriptlang.org/docs/)

## ✨ Features

✅ Python FastAPI backend with REST API
✅ Next.js + React frontend with TypeScript
✅ Local PostgreSQL database (no Docker)
✅ CORS-enabled communication
✅ API documentation (Swagger UI)
✅ Pydantic models for validation
✅ Tailwind CSS styling
✅ In-memory data storage (for learning)

## 🎓 What You'll Learn

- How to build a Python FastAPI backend
- How to create a Next.js + React frontend
- How to communicate between frontend and backend via REST API
- How to structure a full-stack project
- TypeScript basics
- PostgreSQL basics
- API design principles

## 🤝 Contributing

This is a learning tutorial. Feel free to fork and modify!

## 📄 License

MIT

## 🆘 Getting Help

1. Check the `backend/README.md` for backend-specific issues
2. Check the `frontend/README.md` for frontend-specific issues
3. Review the code comments for explanations
4. Check FastAPI and Next.js documentation

---

**Happy Coding! 🚀**
