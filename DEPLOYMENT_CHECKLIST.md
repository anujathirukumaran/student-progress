# Deployment Checklist

## Pre-Deployment Checklist

### Backend Preparation
- [ ] All dependencies listed in package.json
- [ ] .env.example file created
- [ ] .gitignore includes node_modules and .env
- [ ] MongoDB Atlas cluster created and accessible
- [ ] Database user created with read/write permissions
- [ ] IP whitelist configured (0.0.0.0/0 for production)
- [ ] Test all API endpoints locally
- [ ] CORS configured for production URLs

### Frontend Preparation
- [ ] All dependencies listed in package.json
- [ ] .env.example file created
- [ ] .gitignore includes node_modules, dist, and .env
- [ ] Build command works: `npm run build`
- [ ] Preview build works: `npm run preview`
- [ ] All routes tested locally
- [ ] API URL configured for production

### Code Quality
- [ ] No console.errors in production code
- [ ] No hardcoded credentials
- [ ] All sensitive data in environment variables
- [ ] Error handling implemented
- [ ] Loading states implemented
- [ ] Responsive design tested

## GitHub Setup

### Repository Preparation
```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit: Student Progress Tracker"

# Create GitHub repository (via GitHub website)
# Then connect and push:
git remote add origin https://github.com/yourusername/student-progress-tracker.git
git branch -M main
git push -u origin main
```

### Repository Structure
```
✅ README.md present
✅ .gitignore configured
✅ License file (optional)
✅ Documentation files included
```

## Backend Deployment (Render)

### Step-by-Step Render Deployment

1. **Create Render Account**
   - [ ] Go to https://render.com
   - [ ] Sign up with GitHub
   - [ ] Verify email

2. **Create Web Service**
   - [ ] Click "New +" → "Web Service"
   - [ ] Connect GitHub repository
   - [ ] Select your repository

3. **Configure Service**
   ```
   Name: student-progress-backend
   Region: Choose closest to your users
   Branch: main
   Root Directory: backend
   Runtime: Node
   Build Command: npm install
   Start Command: npm start
   ```

4. **Add Environment Variables**
   - [ ] MONGODB_URI: `mongodb+srv://...`
   - [ ] JWT_SECRET: `your-secret-key`
   - [ ] NODE_ENV: `production`
   - [ ] PORT: `5000` (optional, Render sets this)

5. **Deploy**
   - [ ] Click "Create Web Service"
   - [ ] Wait for deployment (5-10 minutes)
   - [ ] Check logs for errors
   - [ ] Test health endpoint: `https://your-app.onrender.com`

6. **Verify Backend**
   - [ ] API responds at root endpoint
   - [ ] MongoDB connection successful
   - [ ] No errors in logs
   - [ ] Copy backend URL for frontend

### Render Configuration File (Optional)
Create `backend/render.yaml`:
```yaml
services:
  - type: web
    name: student-progress-backend
    env: node
    buildCommand: npm install
    startCommand: npm start
    envVars:
      - key: NODE_ENV
        value: production
```

## Frontend Deployment (Vercel)

### Step-by-Step Vercel Deployment

1. **Create Vercel Account**
   - [ ] Go to https://vercel.com
   - [ ] Sign up with GitHub
   - [ ] Verify email

2. **Import Project**
   - [ ] Click "Add New" → "Project"
   - [ ] Import your GitHub repository
   - [ ] Select repository

3. **Configure Project**
   ```
   Framework Preset: Vite
   Root Directory: frontend
   Build Command: npm run build
   Output Directory: dist
   Install Command: npm install
   ```

4. **Add Environment Variables**
   - [ ] Name: `VITE_API_URL`
   - [ ] Value: `https://mern-intern-backend-7381.onrender.com/api`
   - [ ] Environment: Production

5. **Deploy**
   - [ ] Click "Deploy"
   - [ ] Wait for deployment (2-5 minutes)
   - [ ] Check build logs
   - [ ] Visit deployed URL

6. **Verify Frontend**
   - [ ] Home page loads correctly
   - [ ] Navigation works
   - [ ] Can register new user
   - [ ] Can login
   - [ ] Dashboard loads
   - [ ] API calls work

### Vercel Configuration File
Already created: `frontend/vercel.json`
```json
{
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ]
}
```

## Post-Deployment Configuration

### Update Backend CORS
After frontend deployment, update `backend/server.js`:

```javascript
app.use(cors({
  origin: [
    'https://your-vercel-app.vercel.app',
    'http://localhost:5173'  // Keep for local development
  ],
  credentials: true
}));
```

Commit and push to trigger redeployment on Render.

### Test Production Environment
- [ ] Register new user on production
- [ ] Login with new user
- [ ] Test student dashboard
- [ ] Test teacher dashboard
- [ ] Add student progress
- [ ] Verify data persistence
- [ ] Test logout functionality
- [ ] Check login/logout timestamps

## Domain Configuration (Optional)

### Custom Domain for Frontend (Vercel)
1. [ ] Go to Vercel project settings
2. [ ] Click "Domains"
3. [ ] Add your custom domain
4. [ ] Update DNS records as instructed
5. [ ] Wait for SSL certificate

### Custom Domain for Backend (Render)
1. [ ] Go to Render dashboard
2. [ ] Select your service
3. [ ] Click "Settings" → "Custom Domain"
4. [ ] Add your domain
5. [ ] Update DNS records
6. [ ] Update frontend VITE_API_URL

## Monitoring & Maintenance

### Render Monitoring
- [ ] Check deployment logs regularly
- [ ] Monitor response times
- [ ] Set up alerts for downtime
- [ ] Check database connection status

### Vercel Monitoring
- [ ] Check Analytics dashboard
- [ ] Monitor build times
- [ ] Review error logs
- [ ] Check bandwidth usage

### MongoDB Atlas Monitoring
- [ ] Monitor database size
- [ ] Check connection count
- [ ] Review slow queries
- [ ] Set up backup schedule

## Troubleshooting

### Backend Issues

**Build Fails:**
```bash
# Check package.json
# Ensure all dependencies are listed
# Verify Node version compatibility
```

**MongoDB Connection Error:**
- [ ] Check connection string
- [ ] Verify IP whitelist (0.0.0.0/0)
- [ ] Check database user permissions
- [ ] Ensure network access is enabled

**API Not Responding:**
- [ ] Check Render logs
- [ ] Verify environment variables
- [ ] Test endpoints with Postman
- [ ] Check CORS configuration

### Frontend Issues

**Build Fails:**
```bash
# Check for TypeScript errors
# Verify all imports
# Check environment variables
# Test build locally: npm run build
```

**API Connection Error:**
- [ ] Verify VITE_API_URL is correct
- [ ] Check backend is running
- [ ] Verify CORS settings
- [ ] Check browser console for errors

**Routing Issues:**
- [ ] Verify vercel.json is present
- [ ] Check React Router configuration
- [ ] Test all routes manually

## Performance Optimization

### Backend
- [ ] Enable compression
- [ ] Add rate limiting
- [ ] Implement caching
- [ ] Optimize database queries
- [ ] Add indexes to MongoDB

### Frontend
- [ ] Minimize bundle size
- [ ] Lazy load components
- [ ] Optimize images
- [ ] Enable code splitting
- [ ] Add service worker (PWA)

## Security Checklist

- [ ] Environment variables secured
- [ ] No credentials in code
- [ ] HTTPS enabled (automatic on Vercel/Render)
- [ ] JWT secret is strong
- [ ] Password hashing enabled
- [ ] Input validation implemented
- [ ] CORS properly configured
- [ ] Rate limiting added (optional)

## Backup Strategy

### Database Backup
- [ ] Enable MongoDB Atlas automated backups
- [ ] Set backup frequency (daily recommended)
- [ ] Test restore procedure
- [ ] Document backup location

### Code Backup
- [ ] Code in GitHub (version controlled)
- [ ] Multiple branches for safety
- [ ] Tag releases
- [ ] Document deployment process

## Continuous Deployment

### Automatic Deployments
Both Render and Vercel support automatic deployments:

- [ ] Push to main branch triggers deployment
- [ ] Pull requests create preview deployments
- [ ] Failed builds don't affect production
- [ ] Rollback available if needed

### Deployment Workflow
```bash
# Make changes locally
git add .
git commit -m "Description of changes"
git push origin main

# Automatic deployment triggers
# Render: Backend deploys
# Vercel: Frontend deploys
# Wait 5-10 minutes
# Test production site
```

## Final Verification

### Functionality Test
- [ ] User registration works
- [ ] User login works
- [ ] Student dashboard displays correctly
- [ ] Teacher dashboard displays correctly
- [ ] Data updates persist
- [ ] Logout works
- [ ] Activity tracking works

### Performance Test
- [ ] Page load time < 3 seconds
- [ ] API response time < 1 second
- [ ] No console errors
- [ ] Mobile responsive
- [ ] Cross-browser compatible

### Security Test
- [ ] Cannot access protected routes without login
- [ ] Student cannot edit data
- [ ] Teacher can only see their department
- [ ] Passwords are hashed
- [ ] JWT tokens expire correctly

## Success Criteria

Your deployment is successful when:
✅ Frontend loads on Vercel URL
✅ Backend responds on Render URL
✅ Database connection works
✅ User registration works
✅ Login/logout works
✅ All dashboards function correctly
✅ Data persists across sessions
✅ No errors in production logs
✅ Mobile responsive
✅ HTTPS enabled

## Support Resources

- **Render Docs**: https://render.com/docs
- **Vercel Docs**: https://vercel.com/docs
- **MongoDB Atlas**: https://docs.atlas.mongodb.com
- **React Docs**: https://react.dev
- **Express Docs**: https://expressjs.com

## Deployment Timeline

Estimated time for complete deployment:
- Backend setup: 15-20 minutes
- Frontend setup: 10-15 minutes
- Testing: 15-20 minutes
- Total: 40-55 minutes

## Post-Deployment Tasks

- [ ] Share production URL with stakeholders
- [ ] Document any custom configurations
- [ ] Set up monitoring alerts
- [ ] Create user documentation
- [ ] Plan for future updates
- [ ] Schedule regular maintenance

---

**Congratulations! Your Student Progress Tracker is now live! 🎉**
