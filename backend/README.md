# FastAPI Backend Setup (No Docker)

## Prerequisites

- Python 3.9+
- PostgreSQL (local installation)

## Step 1: Install PostgreSQL Locally

### macOS
```bash
brew install postgresql@15
brew services start postgresql@15
```

### Windows
Download and install from: https://www.postgresql.org/download/windows/

### Linux (Ubuntu/Debian)
```bash
sudo apt-get install postgresql postgresql-contrib
sudo service postgresql start
```

## Step 2: Create Database

```bash
# Connect to PostgreSQL
psql -U postgres

# Inside psql prompt:
CREATE DATABASE fullstack_db;
CREATE USER "user" WITH PASSWORD 'password';
ALTER ROLE "user" SET client_encoding TO 'utf8';
ALTER ROLE "user" SET default_transaction_isolation TO 'read committed';
ALTER ROLE "user" SET default_transaction_deferrable TO on;
ALTER ROLE "user" SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE fullstack_db TO "user";
\q
```

## Step 3: Setup Python Backend

```bash
cd backend
python -m venv venv

# On macOS/Linux:
source venv/bin/activate

# On Windows:
venv\Scripts\activate
```

## Step 4: Install Dependencies

```bash
pip install -r requirements.txt
```

## Step 5: Create .env File

```bash
cp .env.example .env
```

Edit `.env` with your PostgreSQL credentials:
```
DATABASE_URL=postgresql://user:password@localhost:5432/fullstack_db
FASTAPI_ENV=development
DEBUG=True
```

## Step 6: Run the Server

```bash
uvicorn app.main:app --reload --port 8000
```

✅ Backend API: http://localhost:8000
📖 API Docs: http://localhost:8000/docs
🔴 ReDoc: http://localhost:8000/redoc

## Troubleshooting

### PostgreSQL Connection Error
- Check if PostgreSQL is running
- Verify credentials in `.env`
- Test connection: `psql -U user -d fullstack_db -h localhost`

### Port 8000 Already in Use
```bash
lsof -i :8000
kill -9 <PID>
```

### Virtual Environment Not Activated
Make sure to activate venv before running commands.
