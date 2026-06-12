# Next.js Frontend Setup (No Database Required Yet)

## Prerequisites

- Node.js 18+
- npm or yarn

## Step 1: Install Dependencies

```bash
cd frontend
npm install
```

## Step 2: Create Environment File

```bash
cp .env.local.example .env.local
```

Edit `.env.local`:
```
NEXT_PUBLIC_API_URL=http://localhost:8000
```

## Step 3: Run Development Server

```bash
npm run dev
```

✅ Frontend: http://localhost:3000

## Project Structure

```
frontend/
├── pages/
│   ├── api/
│   │   └── users.ts          # Proxy to FastAPI
│   ├── _app.tsx              # App wrapper
│   ├── _document.tsx         # HTML structure
│   └── index.tsx             # Home page
├── styles/                   # CSS files
├── package.json
├── tsconfig.json
├── next.config.js
└── README.md
```

## How Communication Works

```
React Component
    ↓ (fetch('/api/users'))
Next.js API Route (pages/api/users.ts)
    ↓ (axios to Python FastAPI)
Python FastAPI Backend (http://localhost:8000/api/users)
```

## Available Scripts

```bash
# Development server
npm run dev

# Production build
npm run build

# Start production server
npm start

# Linting
npm run lint
```

## Troubleshooting

### Port 3000 already in use
```bash
lsof -i :3000
kill -9 <PID>
```

### Can't connect to backend
- Ensure FastAPI is running on port 8000
- Check `NEXT_PUBLIC_API_URL` in `.env.local`

### Node modules issues
```bash
rm -rf node_modules package-lock.json
npm install
```
