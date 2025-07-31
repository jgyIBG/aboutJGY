# Deployment Guide

This guide covers different deployment options for your personal portfolio website.

## Option 1: Vercel (Recommended for Full-Stack)

1. **Create a Vercel account** at [vercel.com](https://vercel.com)

2. **Connect your GitHub repository**:
   - Import your repository from GitHub
   - Vercel will auto-detect it as a Vite project

3. **Configure build settings**:
   - Build Command: `npm run build`
   - Output Directory: `dist/public`
   - Install Command: `npm install`

4. **Environment Variables** (if needed):
   - Add any environment variables in the Vercel dashboard

5. **Deploy**: Vercel will automatically deploy on every push to main branch

## Option 2: Netlify

1. **Create a Netlify account** at [netlify.com](https://netlify.com)

2. **Connect your repository**:
   - Choose "Deploy with Git"
   - Connect your GitHub repository

3. **Build settings**:
   - Build command: `npm run build`
   - Publish directory: `dist/public`

4. **Deploy**: Automatic deployment on every push

## Option 3: GitHub Pages (Static Only)

For static deployment without the backend:

1. **Add deployment workflow**:
Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '20'
          
      - name: Install dependencies
        run: npm install
        
      - name: Build
        run: npm run build:client
        
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist/public
```

2. **Enable GitHub Pages** in repository settings
3. **Set source** to "GitHub Actions"

## Option 4: Custom VPS/Server

1. **Build the application**:
```bash
npm run build
```

2. **Transfer files** to your server

3. **Install dependencies**:
```bash
npm install --production
```

4. **Start the server**:
```bash
npm start
```

5. **Use PM2** for process management:
```bash
npm install -g pm2
pm2 start server/index.js --name "portfolio"
pm2 startup
pm2 save
```

## Domain Configuration

### Custom Domain
1. **Purchase a domain** (e.g., jasonyou.dev)
2. **Configure DNS**:
   - For Vercel: Add CNAME record pointing to `cname.vercel-dns.com`
   - For Netlify: Add CNAME record pointing to your Netlify subdomain
3. **Add domain** in your hosting platform's dashboard
4. **Enable HTTPS** (usually automatic)

### SSL Certificate
Most hosting platforms (Vercel, Netlify) provide automatic SSL certificates. For custom servers, use Let's Encrypt.

## Performance Optimization

### Before Deployment
1. **Optimize images**: Compress images in `attached_assets/`
2. **Review bundle size**: Check for unused dependencies
3. **Test production build** locally with `npm run preview`

### After Deployment
1. **Enable Gzip compression**
2. **Set up CDN** if needed
3. **Monitor performance** with tools like Lighthouse

## Environment Variables

If you need environment variables for production:

### Vercel
Add in Project Settings > Environment Variables

### Netlify
Add in Site Settings > Environment Variables

### Custom Server
Create `.env.production` file:
```
NODE_ENV=production
PORT=3000
```

## Troubleshooting

### Common Issues

1. **Build fails**: Check Node.js version (requires 20+)
2. **Images not loading**: Verify asset paths and imports
3. **404 on refresh**: Configure fallback to `index.html` for SPA routing
4. **Contact form not working**: Backend needed for form functionality

### Vercel Specific
- **Function timeout**: Serverless functions have 10s timeout on hobby plan
- **Bundle size**: Each function must be under 50MB

### Netlify Specific  
- **Build timeout**: Free tier has 15-minute build timeout
- **Bandwidth limits**: Check usage if site gets high traffic

## Monitoring and Analytics

Consider adding:
- **Google Analytics** for visitor tracking
- **Sentry** for error monitoring
- **Uptime monitoring** services

## Backup and Version Control

- **Regular commits** to GitHub
- **Tag releases** for deployment versions
- **Database backups** if using external database