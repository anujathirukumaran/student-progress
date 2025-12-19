# Complete Setup Guide - Student Progress Tracker

## Step-by-Step Installation Guide

### Step 1: MongoDB Atlas Setup

1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free account or login
3. Create a new cluster (Free tier M0 is sufficient)
4. Click "Connect" on your cluster
5. Add your IP address (or use 0.0.0.0/0 for development)
6. Create a database user with username and password
7. Choose "Connect your application"
8. Copy the connection string (looks like: `mongodb+srv://username:<password>@cluster.mongodb.net/`)
9. Replace `<password>` with your actual password
10. Add database name: `mongodb+srv://username:password@cluster.mongodb.net/student_progress`

### Step 2: Backend Setup

```bash
# Navigate to backend folder
cd backend

# Install dependencies
npm install

# Create .env file
# On Windows:
copy .env.example .env

# On Mac/Linux:
cp .env.example .env
```

Edit `.env` file:
```
MONGODB_URI=mongodb+srv://your_username:your_password@cluster.mongodb.net/student_progress
JWT_SECRET=your_super_secret_key_min_32_characters_long
PORT=5000
NODE_ENV=development
```

Start backend:
```bash
npm run dev
```

You should see:
```
Server running on port 5000
MongoDB Connected Successfully
```

### Step 3: Frontend Setup

Open a new terminal:

```bash
# Navigate to frontend folder
cd frontend

# Install dependencies
npm install

# Create .env file
# On Windows:
copy .env.example .env

# On Mac/Linux:
cp .env.example .env
```

Edit `.env` file:
```
VITE_API_URL=https://mern-intern-backend-7381.onrender.com/api
```

Start frontend:
```bash
npm run dev
```

You should see:
```
VITE v7.x.x  ready in xxx ms

➜  Local:   http://localhost:5173/
```

### Step 4: Test the Application

1. Open browser and go to `http://localhost:5173`
2. Click "Register Now"
3. Create a teacher account:
   - Name: John Teacher
   - Email: teacher@test.com
   - Password: password123
   - Role: Staff
   - Department: Computer Science
4. Create a student account (logout first):
   - Name: Jane Student
   - Email: student@test.com
   - Password: password123
   - Role: Student

### Step 5: Test Teacher Features

1. Login as teacher (teacher@test.com)
2. You'll see the Teacher Dashboard
3. Click "Edit Progress" on a student
4. Add attendance, marks, and suggestions
5. Click "Update Progress"

### Step 6: Test Student Features

1. Logout and login as student (student@test.com)
2. You'll see the Student Dashboard
3. View your attendance, marks, and suggestions
4. Note: You cannot edit anything (read-only)

## Deployment Guide

### Deploy Backend to Render

1. Push your code to GitHub
2. Go to [Render](https://render.com)
3. Sign up/Login
4. Click "New +" → "Web Service"
5. Connect your GitHub repository
6. Configure:
   - Name: student-progress-backend
   - Root Directory: `backend`
   - Environment: Node
   - Build Command: `npm install`
   - Start Command: `npm start`
7. Add Environment Variables:
   - `MONGODB_URI`: Your MongoDB Atlas connection string
   - `JWT_SECRET`: Your secret key
   - `NODE_ENV`: production
8. Click "Create Web Service"
9. Wait for deployment (5-10 minutes)
10. Copy your backend URL (e.g., `https://student-progress-backend.onrender.com`)

### Deploy Frontend to Vercel

1. Go to [Vercel](https://vercel.com)
2. Sign up/Login with GitHub
3. Click "Add New" → "Project"
4. Import your GitHub repository
5. Configure:
   - Framework Preset: Vite
   - Root Directory: `frontend`
   - Build Command: `npm run build`
   - Output Directory: `dist`
6. Add Environment Variable:
   - Name: `VITE_API_URL`
   - Value: `https://mern-intern-backend-7381.onrender.com/api`
7. Click "Deploy"
8. Wait for deployment (2-5 minutes)
9. Your app is live!

### Update CORS for Production

After deployment, update backend `server.js`:

```javascript
app.use(cors({
  origin: ['https://your-vercel-app.vercel.app', 'http://localhost:5173'],
  credentials: true
}));
```

Redeploy backend on Render.

## Troubleshooting

### Backend Issues

**MongoDB Connection Error:**
- Check your connection string
- Ensure IP whitelist includes your IP or 0.0.0.0/0
- Verify database user credentials

**Port Already in Use:**
```bash
# Windows
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# Mac/Linux
lsof -ti:5000 | xargs kill -9
```

### Frontend Issues

**API Connection Error:**
- Verify backend is running
- Check VITE_API_URL in .env
- Ensure no CORS errors in browser console

**Module Not Found:**
```bash
rm -rf node_modules package-lock.json
npm install
```

### Deployment Issues

**Render Build Fails:**
- Check build logs
- Ensure all dependencies are in package.json
- Verify Node version compatibility

**Vercel Build Fails:**
- Check environment variables
- Ensure VITE_API_URL is set correctly
- Verify build command is correct

## Common Commands

### Backend
```bash
npm install          # Install dependencies
npm run dev         # Development mode with nodemon
npm start           # Production mode
```

### Frontend
```bash
npm install         # Install dependencies
npm run dev        # Development server
npm run build      # Build for production
npm run preview    # Preview production build
```

## Testing Checklist

- [ ] Backend server starts without errors
- [ ] MongoDB connection successful
- [ ] Frontend loads on localhost:5173
- [ ] Can register as student
- [ ] Can register as teacher with department
- [ ] Can login as student
- [ ] Can login as teacher
- [ ] Student sees dashboard with no data message
- [ ] Teacher sees students list
- [ ] Teacher can edit student progress
- [ ] Student sees updated progress
- [ ] Logout works correctly
- [ ] Login/logout times are tracked

## Support

If you encounter issues:
1. Check the console for error messages
2. Verify all environment variables
3. Ensure MongoDB Atlas is accessible
4. Check network connectivity
5. Review the README.md for additional information

## Next Steps

After successful setup:
1. Customize the UI colors and branding
2. Add more fields to student progress
3. Implement email notifications
4. Add data export features
5. Create admin dashboard
6. Add charts and analytics
