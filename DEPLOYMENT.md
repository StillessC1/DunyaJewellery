# Render Deployment Guide

## 🚀 Deploy Dunya Jewellery to Render with Persistent Database

### Step 1: Connect Your Repository
1. Go to [render.com](https://render.com)
2. Sign up/login with your GitHub account
3. Click **"New +"** → **"Web Service"**
4. Connect your GitHub repository: `StillessC1/DunyaJewellery`

### Step 2: Configure Backend Service
1. **Name**: `dunya-jewellery-backend`
2. **Environment**: `Python 3`
3. **Root Directory**: `backend`
4. **Build Command**: `pip install -r requirements.txt`
5. **Start Command**: `python manage.py migrate && python manage.py runserver 0.0.0.0:$PORT`
6. **Instance Type**: `Free`

### Step 3: Add Environment Variables
Add these environment variables:
- `SECRET_KEY`: Generate a secure key (Render can auto-generate)
- `DEBUG`: `false`
- `ALLOWED_HOSTS`: `.onrender.com`
- `TELEGRAM_BOT_TOKEN`: Your Telegram bot token
- `TELEGRAM_CHAT_ID`: Your Telegram chat ID
- `TELEGRAM_USERNAME`: Your Telegram username

### Step 4: Create PostgreSQL Database
1. In your Render dashboard, click **"New +"** → **"PostgreSQL"**
2. **Name**: `dunya-jewellery-db`
3. **Database Name**: `dunya_jewellery`
4. **User**: `dunya_user`
5. **Plan**: `Free`
6. Click **"Create Database"**

### Step 5: Connect Database to Backend
1. Go back to your backend service settings
2. Add environment variable:
   - `DATABASE_URL`: Connect to your `dunya-jewellery-db` database
3. Restart your backend service

### Step 6: Deploy Frontend
1. Click **"New +"** → **"Static Site"**
2. **Name**: `dunya-jewellery-frontend`
3. **Root Directory**: `frontend`
4. **Build Command**: `npm run build`
5. **Publish Directory**: `dist`
6. **Add Environment Variable**:
   - `VITE_API_URL`: Your backend URL (e.g., `https://dunya-jewellery-backend.onrender.com`)

### Step 7: Update Frontend API URL
After deployment, update the frontend API URL:
1. Go to `frontend/src/utils/api.ts`
2. Replace `localhost:8000` with your Render backend URL
3. Commit and push the changes

## 🗄️ Database Persistence

Your PostgreSQL database will persist:
- ✅ Products (won't be deleted on redeploy)
- ✅ Orders and customer data
- ✅ Admin users
- ✅ All Django migrations

## 🔧 Important Notes

1. **Free Tier Limitations**:
   - Apps spin down after 15 minutes of inactivity
   - Cold starts take ~30 seconds
   - Database has 90-day inactivity limit

2. **Telegram Integration**:
   - Make sure your Telegram bot token is set correctly
   - Test notifications after deployment

3. **Static Files**:
   - Django static files are served via Whitenoise
   - No additional configuration needed

## 🌐 Access Your App

After deployment:
- **Backend**: `https://dunya-jewellery-backend.onrender.com`
- **Frontend**: `https://dunya-jewellery-frontend.onrender.com`
- **Admin Panel**: `https://dunya-jewellery-backend.onrender.com/admin`

## 🔄 Automatic Deploys

Enable automatic deploys in Render:
1. Go to your service settings
2. Enable **"Auto-Deploy"**
3. Push changes to GitHub → automatic deployment

## 📱 Testing

1. Visit your frontend URL
2. Add products to test persistence
3. Check admin panel for data
4. Test Telegram notifications
