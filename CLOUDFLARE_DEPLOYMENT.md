# Deploy HiAnime API to Cloudflare Workers

This guide will help you deploy the HiAnime API to Cloudflare Workers for free.

## Prerequisites

- A Cloudflare account (free): https://dash.cloudflare.com/sign-up
- Git installed on your system
- A GitHub account

## Step 1: Push to GitHub

1. **Create a new GitHub repository:**
   - Go to https://github.com/new
   - Name it: `hianime-api`
   - Keep it **Public** or **Private** (your choice)
   - **DO NOT** initialize with README (already have files)
   - Click "Create repository"

2. **Add the remote and push:**
   ```bash
   cd c:\Users\chenk\OneDrive\Desktop\anime\hianime-api
   git remote add origin https://github.com/YOUR_USERNAME/hianime-api.git
   git branch -M main
   git push -u origin main
   ```

## Step 2: Deploy to Cloudflare Workers

### Option A: Using Wrangler CLI (Recommended)

1. **Install Wrangler globally:**
   ```bash
   npm install -g wrangler
   ```

2. **Login to Cloudflare:**
   ```bash
   wrangler login
   ```
   This will open a browser window for authentication.

3. **Deploy the worker:**
   ```bash
   cd c:\Users\chenk\OneDrive\Desktop\anime\hianime-api
   wrangler deploy
   ```

4. **Your API will be live at:**
   ```
   https://hianime-api.YOUR_SUBDOMAIN.workers.dev
   ```

### Option B: Using Cloudflare Dashboard

1. **Go to Cloudflare Dashboard:**
   - Visit: https://dash.cloudflare.com
   - Navigate to: Workers & Pages > Create application > Create Worker

2. **Deploy from GitHub:**
   - Connect your GitHub account
   - Select the `hianime-api` repository
   - Click "Deploy"

## Step 3: Configure Environment Variables (Optional)

If you want Redis caching (recommended), set up Upstash:

1. **Get Redis URL:**
   - Go to https://upstash.com (free tier available)
   - Create a Redis database
   - Copy the REST URL and Token

2. **Add to Cloudflare:**
   - In Cloudflare Dashboard > Workers > Your Worker > Settings > Variables
   - Add:
     - `UPSTASH_REDIS_REST_URL`: Your Redis URL
     - `UPSTASH_REDIS_REST_TOKEN`: Your Redis Token
     - `ORIGIN`: `*` (or your frontend domain)

## Step 4: Test Your Deployment

Once deployed, test the API:

```bash
# Test home endpoint
curl https://YOUR_WORKER_URL.workers.dev/api/v1/home

# Test anime list
curl https://YOUR_WORKER_URL.workers.dev/api/v1/animes/top-airing?page=1
```

## Step 5: Update Your Frontend

Update your frontend to use the deployed API:

```javascript
// In c:\Users\chenk\OneDrive\Desktop\anime\anime-webapp\frontend\src\lib\api.js
const API_BASE_URL = 'https://YOUR_WORKER_URL.workers.dev/api/v1';
```

## Troubleshooting

### Deployment Fails
- Make sure `wrangler.toml` exists in the root
- Check your Cloudflare account has Workers enabled
- Verify you're logged in: `wrangler whoami`

### API Returns Errors
- Check Cloudflare Workers logs in the dashboard
- Verify environment variables are set correctly
- Make sure Redis URL is valid (if using)

### CORS Issues
- Add `ORIGIN=*` environment variable
- Or set it to your frontend domain for security

## Free Tier Limits

Cloudflare Workers Free Tier:
- ✅ 100,000 requests/day
- ✅ 10ms CPU time per request
- ✅ Unlimited bandwidth
- ✅ Global CDN

This is MORE than enough for personal use!

## Next Steps

After successful deployment:

1. ✅ Update frontend API URL to your Cloudflare Workers URL
2. ✅ Test all endpoints work from your web app
3. ✅ Use the same URL for your Android Kotlin app
4. ✅ Monitor usage in Cloudflare Dashboard

## Support

If you encounter issues:
- Check HiAnime API docs: https://github.com/ryanwtf88/hianime-api
- Cloudflare Workers docs: https://developers.cloudflare.com/workers
- Wrangler docs: https://developers.cloudflare.com/workers/wrangler

---

**Your API is ready to deploy! Follow the steps above and you'll have a working anime API in minutes!** 🚀
