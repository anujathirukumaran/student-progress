# Quick Start Guide

## Prerequisites
- Node.js installed (v18+)
- MongoDB Atlas account created
- Git installed

## 5-Minute Setup

### 1. Backend Setup (2 minutes)

```bash
# Terminal 1
cd backend
npm install
```

Create `backend/.env`:
```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/student_progress
JWT_SECRET=my_super_secret_jwt_key_12345678
PORT=5000
NODE_ENV=development
```

```bash
npm run dev
```

### 2. Frontend Setup (2 minutes)

```bash
# Terminal 2 (new terminal)
cd frontend
npm install
```

Create `frontend/.env`:
```
VITE_API_URL=http://localhost:5000/api
```

```bash
npm run dev
```

### 3. Test (1 minute)

Open browser: `http://localhost:5173`

**Create Teacher Account:**
- Email: teacher@test.com
- Password: test123
- Role: Staff
- Department: Computer Science

**Create Student Account:**
- Email: student@test.com
- Password: test123
- Role: Student

**Test Flow:**
1. Login as teacher
2. Click "Edit Progress" on student
3. Add attendance: 20 total, 18 attended
4. Add marks: Math, 85/100, Mid-term
5. Add suggestion: "Great progress!"
6. Logout
7. Login as student
8. View your progress!

## Project URLs

- Frontend: http://localhost:5173
- Backend: http://localhost:5000
- API Docs: http://localhost:5000/api

## Key Features to Test

✅ Registration with role selection
✅ Login/Logout
✅ Student Dashboard (read-only)
✅ Teacher Dashboard (edit access)
✅ Attendance tracking
✅ Marks management
✅ Suggestions/Feedback
✅ Activity logging (login/logout times)

## Deployment

**Backend (Render):**
1. Push to GitHub
2. Create Web Service on Render
3. Set root: `backend`
4. Add env vars
5. Deploy

**Frontend (Vercel):**
1. Import GitHub repo
2. Set root: `frontend`
3. Add `VITE_API_URL` env var
4. Deploy

## Need Help?

Check `SETUP_GUIDE.md` for detailed instructions.
Check `README.md` for full documentation.

## Common Issues

**MongoDB Connection Failed:**
- Check connection string
- Whitelist IP: 0.0.0.0/0

**Port 5000 in use:**
```bash
# Windows
netstat -ano | findstr :5000
taskkill /PID <PID> /F
```

**CORS Error:**
- Ensure backend is running
- Check VITE_API_URL in frontend/.env

## Tech Stack

- **Frontend:** React 19 + Vite + Axios
- **Backend:** Node.js + Express + MongoDB
- **Auth:** JWT + bcryptjs
- **Deployment:** Vercel + Render

Enjoy building! 🚀
