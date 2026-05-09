# Custom Domain & Email Setup Guide

## Vercel Custom Domain Setup (Web Dashboard)

### Step 1: Add Custom Domain to Vercel
1. Go to your Vercel dashboard: https://vercel.com/dashboard
2. Select your `EDU_TASK` project
3. Go to **Settings → Domains**
4. Click **Add Custom Domain**
5. Enter: `edu-task.bd`
6. Click **Add Domain**

### Step 2: Configure DNS Records
Vercel will provide you with DNS records. Add these to your domain registrar:

```
Type: CNAME
Name: @
Value: cname.vercel-dns.com
TTL: 300

Type: CNAME  
Name: www
Value: cname.vercel-dns.com
TTL: 300
```

### Step 3: Verify Domain
1. Wait for DNS propagation (5-30 minutes)
2. Vercel will automatically verify the domain
3. Your app will be available at: `https://edu-task.bd`

## Resend Email Service Setup

### Step 1: Install Resend CLI (Optional)
```bash
npm install -g resend
```

### Step 2: Add Custom Domain to Resend
1. Go to https://resend.com/domains
2. Click **Add Domain**
3. Enter: `edu-task.bd`
4. Click **Add Domain**

### Step 3: Verify Domain Ownership
Resend will provide DNS records to verify ownership:

```
Type: TXT
Name: _resend
Value: resendsite=abff9026-9ef9-4cce-81b6-c089a1d32f27
TTL: 300
```

### Step 4: Configure Email Sending
After domain verification, update your environment variables:

```env
# Update in Vercel Dashboard → Project Settings → Environment Variables
RESEND_API_KEY=re_xxxxxxxxx
NEXT_PUBLIC_APP_URL=https://edu-task.bd
```

### Step 5: Update Email From Address
Update your email sending code to use verified domain:

```typescript
// In lib/auth/otp.ts
from: 'EduTask <noreply@edu-task.bd>'
```

## Resend API Commands (If Using CLI)

### Add Domain
```bash
resend domains.create({ name: 'edu-task.bd' })
```

### Get Domain Info
```bash
resend domains.get('abff9026-9ef9-4cce-81b6-c089a1d32f27')
```

### Verify Domain
```bash
resend domains.verify('abff9026-9ef9-4cce-81b6-c089a1d32f27')
```

### Update Domain Settings
```bash
resend domains.update({
  id: 'abff9026-9ef9-4cce-81b6-c089a1d32f27',
  openTracking: false,
  clickTracking: true,
})
```

### List All Domains
```bash
resend domains.list()
```

### Delete Domain
```bash
resend domains.remove('abff9026-9ef9-4cce-81b6-c089a1d32f27')
```

## Environment Variables Update

Update your Vercel environment variables:

```env
# Application URLs
NEXT_PUBLIC_APP_URL=https://edu-task.bd
NEXT_PUBLIC_BACKEND_URL=http://localhost:4000
NEXT_PUBLIC_API_BASE_URL=http://127.0.0.1:5000

# Supabase Configuration (unchanged)
NEXT_PUBLIC_SUPABASE_URL=https://pxktjtedpgolzjagkpob.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

# Email Service
RESEND_API_KEY=re_TXhWm7QU_LaAeJsBPjXQLpt4pufSYanWK

# Environment
NODE_ENV=production
```

## Testing Checklist

### After Setup:
- [ ] Domain resolves to `https://edu-task.bd`
- [ ] SSL certificate is active
- [ ] Email sending works with `noreply@edu-task.bd`
- [ ] Registration flow works on custom domain
- [ ] OTP emails are delivered successfully

## Troubleshooting

### DNS Issues:
- Use DNS checker: https://www.whatsmydns.net/
- Wait up to 24 hours for full propagation
- Check with domain registrar if records are correct

### Email Issues:
- Verify domain is verified in Resend dashboard
- Check SPF/DKIM records in DNS
- Monitor Resend dashboard for delivery status

### Vercel Issues:
- Check Vercel dashboard for deployment logs
- Ensure environment variables are set correctly
- Verify custom domain is properly configured

## Support Links
- Vercel Domains: https://vercel.com/docs/concepts/projects/domains
- Resend Domains: https://resend.com/docs/domains
- DNS Help: Contact your domain registrar
