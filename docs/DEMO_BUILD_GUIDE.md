# Demo Application Build Guide

This guide is specifically for building the application as a **demo/prototype** with mock data enabled.

## Overview

The application is configured as a demo with:
- ✅ Mock Service Worker (MSW) enabled in production
- ✅ Crime Analytics Hub with mock data
- ✅ All features functional without backend
- ✅ Production optimizations applied

## Quick Demo Build

### Windows PowerShell
```powershell
# Create production environment file with MSW enabled
@"
VITE_APP_ENV=production
VITE_API_BASE_URL=http://localhost:5128/api
VITE_ENABLE_MSW=true
VITE_ENABLE_ANALYTICS=false
VITE_ENABLE_ERROR_TRACKING=false
VITE_APP_NAME=Central Co-op Interactive Portal (Demo)
VITE_APP_VERSION=1.0.0
"@ | Out-File -FilePath .env.production -Encoding utf8

# Build
npm run build:production

# Preview
npm run preview
```

### Windows CMD
```cmd
(
echo VITE_APP_ENV=production
echo VITE_API_BASE_URL=http://localhost:5128/api
echo VITE_ENABLE_MSW=true
echo VITE_ENABLE_ANALYTICS=false
echo VITE_APP_NAME=Central Co-op Interactive Portal (Demo^)
echo VITE_APP_VERSION=1.0.0
) > .env.production

npm run build:production
npm run preview
```

### Linux/Mac
```bash
cat > .env.production << EOF
VITE_APP_ENV=production
VITE_API_BASE_URL=http://localhost:5128/api
VITE_ENABLE_MSW=true
VITE_ENABLE_ANALYTICS=false
VITE_ENABLE_ERROR_TRACKING=false
VITE_APP_NAME=Central Co-op Interactive Portal (Demo)
VITE_APP_VERSION=1.0.0
EOF

npm run build:production
npm run preview
```

## Deploy as Demo

### Vercel (with MSW enabled)

1. Push your code to GitHub

2. Import project in Vercel

3. Configure environment variables in Vercel dashboard:
   ```
   VITE_APP_ENV=production
   VITE_ENABLE_MSW=true
   VITE_API_BASE_URL=http://localhost:5128/api
   VITE_APP_NAME=Central Co-op Interactive Portal (Demo)
   ```

4. Deploy!

### Netlify (with MSW enabled)

1. Push your code to GitHub

2. Import project in Netlify

3. Configure environment variables in Netlify dashboard:
   ```
   VITE_APP_ENV=production
   VITE_ENABLE_MSW=true
   VITE_API_BASE_URL=http://localhost:5128/api
   VITE_APP_NAME=Central Co-op Interactive Portal (Demo)
   ```

4. Deploy!

## What Works in Demo Mode

With MSW enabled, all these features work with mock data:

### ✅ Crime Analytics Hub
- Historical crime data visualization
- Trend analysis
- Geographic distribution
- Time-based patterns
- Category breakdowns

### ✅ Dashboard Features
- Real-time statistics (simulated)
- Charts and graphs
- Activity feeds
- Alert notifications

### ✅ CRUD Operations
- Create incidents
- Update records
- Delete items
- Search and filter

### ✅ User Management
- Login/authentication (mock)
- Role-based access
- User profiles

### ✅ Customer Management
- Customer listings
- Site management
- Region assignment

## Verify Demo Mode

After deployment, check that MSW is running:

1. Open browser console
2. Look for: `[MSW] Mocking enabled.`
3. Check: `console.log(import.meta.env.VITE_ENABLE_MSW)` should return `"true"`

## Demo vs Production Toggle

You can easily switch between demo and production:

### Enable Demo Mode (MSW ON)
```bash
# In .env.production
VITE_ENABLE_MSW=true
```

### Enable Production Mode (MSW OFF)
```bash
# In .env.production
VITE_ENABLE_MSW=false
VITE_API_BASE_URL=https://your-real-api.com/api
```

Then rebuild:
```bash
npm run build:production
```

## Performance Notes

**Demo mode does NOT impact performance:**
- ✅ Code splitting still works
- ✅ Bundle optimization applied
- ✅ Lazy loading active
- ✅ Production minification
- ✅ Console logs removed (except MSW init)

The only difference is data source (mocked vs real API).

## Troubleshooting

### MSW Not Working in Production
**Check:**
1. `VITE_ENABLE_MSW=true` in `.env.production`
2. `mockServiceWorker.js` exists in `public/` folder
3. Browser console shows no service worker errors

**Fix:**
```bash
# Regenerate MSW worker
npx msw init public/ --save

# Rebuild
npm run build:production
```

### Mock Data Not Showing
**Verify MSW handlers:**
1. Check `src/mocks/handlers.ts` exists
2. Ensure handlers are properly imported in `src/mocks/browser.ts`
3. Clear browser cache and reload

## Adding More Mock Data

To add more mock endpoints for demo:

1. Edit `src/mocks/handlers.ts`
2. Add new request handlers:
   ```typescript
   http.get('/api/new-endpoint', () => {
     return HttpResponse.json({
       data: [...mockData]
     })
   })
   ```
3. Rebuild

## Demo Presentation Tips

When presenting the demo:

1. **Highlight Real Features**: All UI/UX is production-ready
2. **Explain Mock Data**: Makes demo self-contained
3. **Show Responsiveness**: Works on all devices
4. **Demonstrate Speed**: Production build is fast
5. **Note Scalability**: Easy switch to real backend

## Transition to Production

When backend is ready, simply:

1. Update `.env.production`:
   ```env
   VITE_ENABLE_MSW=false
   VITE_API_BASE_URL=https://your-real-api.com/api
   ```

2. Rebuild and redeploy

No code changes needed! 🎉

---

**This is a demo application with mock data enabled for demonstration purposes.**
