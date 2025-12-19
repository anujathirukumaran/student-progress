# Student Progress Tracker

A full-stack web application for tracking student progress with role-based dashboards for students and teachers.

## Features

### Student Features
- View attendance summary
- View marks and exam results
- Receive suggestions and feedback from teachers
- View overall performance evaluation
- Read-only access to all data

### Teacher Features
- Department-based access control
- Add and update student progress data
- Track student attendance
- Add marks for different subjects and exams
- Provide suggestions and feedback
- View student login/logout activity
- Edit student progress information

## Tech Stack

### Frontend
- React 19 with Vite
- React Router DOM for navigation
- Axios for API calls
- Modern CSS with responsive design

### Backend
- Node.js with Express
- MongoDB Atlas with Mongoose
- JWT authentication
- bcryptjs for password hashing
- Role-based access control

## Installation

### Prerequisites
- Node.js (v18 or higher)
- MongoDB Atlas account
- npm or yarn

### Backend Setup

1. Navigate to backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file:
```bash
cp .env.example .env
```

4. Update `.env` with your MongoDB Atlas connection string:
```
MONGODB_URI=your_mongodb_atlas_connection_string
JWT_SECRET=your_secure_jwt_secret
PORT=5000
NODE_ENV=development
```

5. Start the backend server:
```bash
npm run dev
```

Backend will run on `http://localhost:5000`

### Frontend Setup

1. Navigate to frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file:
```bash
cp .env.example .env
```

4. Update `.env`:
```
VITE_API_URL=https://mern-intern-backend-7381.onrender.com
```

5. Start the development server:
```bash
npm run dev
```

Frontend will run on `http://localhost:5173`

## Deployment

### Backend Deployment (Render)

1. Create a new Web Service on Render
2. Connect your GitHub repository
3. Set the following:
   - Build Command: `cd backend && npm install`
   - Start Command: `cd backend && npm start`
4. Add environment variables:
   - `MONGODB_URI`
   - `JWT_SECRET`
   - `NODE_ENV=production`

### Frontend Deployment (Vercel)

1. Install Vercel CLI:
```bash
npm install -g vercel
```

2. Navigate to frontend directory and deploy:
```bash
cd frontend
vercel
```

3. Set environment variable in Vercel dashboard:
   - `VITE_API_URL=https://mern-intern-backend-7381.onrender.com`

4. Or use Vercel dashboard:
   - Import your GitHub repository
   - Set root directory to `frontend`
   - Add environment variable `VITE_API_URL`

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user
- `GET /api/auth/profile` - Get user profile

### Progress Management
- `GET /api/progress/my-progress` - Get student's own progress (Student)
- `GET /api/progress/student/:studentId` - Get specific student progress (Teacher)
- `PUT /api/progress/student/:studentId` - Update student progress (Teacher)
- `GET /api/progress/students` - Get all students by department (Teacher)
- `GET /api/progress/departments` - Get all departments

## Usage

### Registration
1. Navigate to Registration page
2. Fill in: Name, Email, Password
3. Select Role: Student or Staff
4. If Staff, enter Department name
5. Click Register

### Login
1. Enter email and password
2. Click Login
3. Redirected to appropriate dashboard based on role

### Student Dashboard
- View attendance percentage
- See all marks and exam results
- Read teacher suggestions
- View overall performance rating

### Teacher Dashboard
- View all students in your department
- See student login/logout times
- Click "Edit Progress" to update student data:
  - Update attendance
  - Add new marks
  - Add suggestions/feedback
  - Set overall performance rating

## Project Structure

```
PROGRESS_STUDENT/
├── backend/
│   ├── config/
│   │   └── db.js
│   ├── controllers/
│   │   ├── authController.js
│   │   └── progressController.js
│   ├── middleware/
│   │   └── auth.js
│   ├── models/
│   │   ├── User.js
│   │   └── StudentProgress.js
│   ├── routes/
│   │   ├── authRoutes.js
│   │   └── progressRoutes.js
│   ├── .env
│   ├── package.json
│   └── server.js
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   └── Navbar.jsx
│   │   ├── context/
│   │   │   └── AuthContext.jsx
│   │   ├── pages/
│   │   │   ├── Home.jsx
│   │   │   ├── Login.jsx
│   │   │   ├── Register.jsx
│   │   │   ├── StudentDashboard.jsx
│   │   │   └── TeacherDashboard.jsx
│   │   ├── services/
│   │   │   └── api.js
│   │   ├── styles/
│   │   │   └── index.css
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── .env
│   ├── package.json
│   └── vercel.json
└── README.md
```

## Security Features
- Password hashing with bcryptjs
- JWT token-based authentication
- Role-based access control
- Protected API routes
- Secure HTTP headers with CORS

## Contributing
Feel free to submit issues and enhancement requests!

## License
MIT License
