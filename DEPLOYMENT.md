# 🚀 Quick Deployment Guide

## 📦 Push to GitHub

### 1. Install Git
Download from: https://git-scm.com/download/windows

### 2. Configure Git
```powershell
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 3. Initialize Repository
```powershell
cd C:\Users\DELL\.gemini\antigravity\scratch\statistical-viz-platform

git init
git add .
git commit -m "Initial commit: Statistical visualization platform"
```

### 4. Create GitHub Repository
1. Go to https://github.com/new
2. Name: `statistical-viz-platform`
3. Don't initialize with README
4. Create repository

### 5. Push to GitHub
```powershell
# Replace YOUR_USERNAME with your GitHub username
git remote add origin https://github.com/YOUR_USERNAME/statistical-viz-platform.git
git branch -M main
git push -u origin main
```

---

## ☁️ Deploy Backend (Render - Free)

### 1. Create Account
Sign up at https://render.com (use GitHub)

### 2. Create PostgreSQL Database
- Dashboard → **New +** → **PostgreSQL**
- Name: `statistical-viz-db`
- Plan: **Free** (1GB)
- Create Database
- **Save connection details!**

### 3. Create Web Service
- Dashboard → **New +** → **Web Service**
- Connect your GitHub repository
- Root Directory: `backend`
- Name: `statistical-viz-api`
- Environment: **Node**
- Build Command: `npm install`
- Start Command: `npm start`
- Plan: **Free**

### 4. Add Environment Variables
In Render web service settings:
```
DB_HOST=<from database internal URL>
DB_PORT=5432
DB_NAME=statistical_viz
DB_USER=<from database>
DB_PASSWORD=<from database>
API_KEY=579b464db66ec23bdd0000016f0c9a9cc55149755ab16cfd9a231e7d
PORT=3001
NODE_ENV=production
```

### 5. Deploy
- Click **Create Web Service**
- Wait for deployment (2-3 minutes)

### 6. Setup Database
- In Render dashboard → Your web service → **Shell**
- Run: `npm run setup`

### 7. Your API is Live! 🎉
URL: `https://statistical-viz-api.onrender.com`

Test: `https://statistical-viz-api.onrender.com/api/summary`

---

## 🌐 Deploy Frontend (Netlify - Free)

### Option 1: Drag & Drop
1. Go to https://netlify.com
2. Sign up (use GitHub)
3. Drag `frontend` folder to Netlify
4. Done!

### Option 2: GitHub Integration
1. Go to https://netlify.com
2. **New site from Git**
3. Connect GitHub
4. Choose repository
5. Base directory: `frontend`
6. Publish directory: `frontend`
7. Deploy!

### Update API URL
Edit `frontend/index-backend.html`:
```javascript
const API_URL = 'https://statistical-viz-api.onrender.com';
```

---

## ✅ Checklist

- [ ] Git installed
- [ ] Code pushed to GitHub
- [ ] Render account created
- [ ] PostgreSQL database created
- [ ] Backend deployed
- [ ] Environment variables set
- [ ] Database schema setup
- [ ] Frontend deployed
- [ ] API URL updated in frontend
- [ ] Test everything!

---

## 🐛 Troubleshooting

**Git not found**
```powershell
# Install Git, restart PowerShell
git --version
```

**Authentication failed**
- Use Personal Access Token from https://github.com/settings/tokens
- Use as password when pushing

**Backend won't start**
- Check environment variables
- Check database connection
- View logs in Render dashboard

**Frontend can't connect to API**
- Check API URL in frontend code
- Check CORS settings in backend
- Check API is running

---

## 📞 Need Help?

- Backend details: See `backend/README.md`
- Render docs: https://render.com/docs
- Netlify docs: https://docs.netlify.com

---

**Your app will be live in ~30 minutes!** 🚀
