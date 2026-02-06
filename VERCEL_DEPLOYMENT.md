# Vercel Deployment Guide

## 🚀 Deploy Dunya Jewellery to Vercel

### Step 1: Deploy Backend on Render First
Перед деплоем фронтенда на Vercel, сначала задеплойте бэкенд на Render:
- Backend URL: `https://dunya-jewellery-backend.onrender.com`

### Step 2: Deploy Frontend to Vercel

1. **Зайдите на [vercel.com](https://vercel.com)**
2. **Import GitHub Repository**: `StillessC1/DunyaJewellery`
3. **Framework Preset**: `Vite`
4. **Root Directory**: `frontend`
5. **Build Command**: `npm run build`
6. **Output Directory**: `dist`

### Step 3: Environment Variables на Vercel

Добавьте эти переменные в Vercel:

```
VITE_API_BASE_URL=https://dunya-jewellery-backend.onrender.com
```

### Step 4: Deploy

Нажмите **Deploy** и дождитесь окончания сборки.

## 🔧 Environment Variables для Vercel

| Variable | Value | Описание |
|----------|-------|---------|
| `VITE_API_BASE_URL` | `https://dunya-jewellery-backend.onrender.com` | URL вашего бэкенда на Render |

## 📱 Альтернативный вариант (Backend на Vercel)

Если хотите задеплоить и бэкенд на Vercel:

### 1. Создайте `api/index.js` в корне:
```javascript
const express = require('express');
const { execSync } = require('child_process');
const path = require('path');

const app = express();

// Запуск Django сервера
app.use('/api', (req, res) => {
  // Proxy запросы к Django
});

app.listen(process.env.PORT || 3000);
```

### 2. Environment Variables для Backend:
```
DJANGO_SETTINGS_MODULE=config.settings
SECRET_KEY=your_secret_key
DEBUG=false
ALLOWED_HOSTS=.vercel.app
DATABASE_URL=your_postgres_url
```

## 🌐 URLs после деплоя

- **Frontend**: `https://dunya-jewellery.vercel.app`
- **Backend**: `https://dunya-jewellery-backend.onrender.com`
- **Admin**: `https://dunya-jewellery-backend.onrender.com/admin`

## ⚡ Важные моменты

1. **CORS**: Убедитесь что ваш бэкенд разрешает запросы с Vercel домена
2. **Environment Variables**: Все переменные с префиксом `VITE_` доступны в фронтенде
3. **Build**: Vercel автоматически соберет ваш React/TypeScript проект
4. **Preview**: Каждый pull request создает preview деплой

## 🔥 Автоматические деплои

Включите в настройках Vercel:
- **GitHub Integration** → автоматические деплои при push в main
- **Preview Deployments** → деплои для каждого PR
