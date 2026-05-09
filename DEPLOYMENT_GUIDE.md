# EduTask Vercel Deployment Guide

## Prerequisites
- GitHub repository: https://github.com/SUMON-0DEV/EDU_TASK ✅ (Already created)
- Vercel account (free tier works fine)

## Step 1: Connect Vercel to GitHub
1. Go to https://vercel.com
2. Click "Sign Up" or "Login"
3. Choose "Continue with GitHub"
4. Authorize Vercel to access your GitHub account
5. Select your `EDU_TASK` repository from the list

## Step 2: Configure Project Settings
### Build Settings
- **Framework Preset**: Next.js
- **Root Directory**: `edutask-frontend`
- **Build Command**: `npm run build`
- **Install Command**: `npm install`
- **Output Directory**: `.next`

### Environment Variables
Add these in Vercel dashboard → Project Settings → Environment Variables:

```env
# Supabase Configuration
NEXT_PUBLIC_SUPABASE_URL=https://pxktjtedpgolzjagkpob.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InB4a3RqdGVkcGdvbHpqYWdrcG9iIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzgzMzI1NDksImV4cCI6MjA5MzkwODU0OX0.v35RERf1D-BKE3tNLwb12AUxdzO-bCZpRnhf4Qbylwo
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InB4a3RqdGVkcGdvbHpqYWdrcG9iIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc3ODMzMjU0OSwiZXhwIjoyMDkzOTA4NTQ5fQ.KdesTTRdxlaOPh45MUiSvfW_ia01M7Qh1vz2VDipiLI

# Email Service (Resend)
RESEND_API_KEY=re_TXhWm7QU_LaAeJsBPjXQLpt4pufSYanWK

# Application URLs
NEXT_PUBLIC_APP_URL=https://your-vercel-domain.vercel.app
NEXT_PUBLIC_BACKEND_URL=http://localhost:4000
NEXT_PUBLIC_API_BASE_URL=http://127.0.0.1:5000

# Environment
NODE_ENV=production
```

## Step 3: Deploy
1. Click "Deploy" button
2. Vercel will automatically:
   - Clone your repository
   - Install dependencies
   - Build the application
   - Deploy to global CDN

## Step 4: Post-Deployment
### Update Environment Variables
After deployment, update `NEXT_PUBLIC_APP_URL` to your actual Vercel domain.

### Test the Application
1. Visit your Vercel URL
2. Test user registration
3. Verify email functionality (check console for OTP codes)
4. Test complete authentication flow

## Troubleshooting
### Build Errors
- Check `package.json` has correct build script
- Ensure all dependencies are in `package.json`

### Environment Variable Issues
- Double-check all variable names match exactly
- Ensure no extra spaces or quotes
- Verify Supabase keys are correct

### Database Connection Issues
- Ensure Supabase project is active
- Check RLS policies allow access
- Verify CORS settings in Supabase

## Production Considerations
1. **Email Service**: Configure proper domain in Resend for production
2. **Database**: Ensure Supabase has proper quotas
3. **Security**: Review RLS policies before going live
4. **Performance**: Monitor Vercel analytics for optimization

## Deployment URL
Your app will be available at: `https://edutask-frontend-<random-hash>.vercel.app`

## Support
- Vercel Docs: https://vercel.com/docs
- Next.js Deployment: https://vercel.com/docs/frameworks/nextjs
- Supabase Integration: https://supabase.com/docs/guides/with-nextjs
