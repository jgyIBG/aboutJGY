# 🚀 Quick Deploy Instructions

## Step 1: Create GitHub Repository

1. Go to [GitHub](https://github.com) and create a new repository
2. Name it something like `jason-you-portfolio` or `portfolio`
3. Make it **public** (required for GitHub Pages free tier)
4. Don't initialize with README (we'll upload our files)

## Step 2: Upload Your Code

### Option A: Using GitHub Web Interface
1. Click "uploading an existing file" on the repository page
2. Drag and drop ALL files from your project folder
3. Commit the files

### Option B: Using Git Commands
```bash
git init
git add .
git commit -m "Initial commit - Personal portfolio website"
git branch -M main
git remote add origin https://github.com/[YOUR-USERNAME]/[REPOSITORY-NAME].git
git push -u origin main
```

## Step 3: Quick Deploy Options

### 🟢 EASIEST: Vercel (Recommended)
1. Go to [vercel.com](https://vercel.com) and sign up with GitHub
2. Click "New Project" and import your repository
3. Build settings are auto-detected, just click "Deploy"
4. ✅ Your site will be live in 2-3 minutes!

### 🟡 Alternative: Netlify
1. Go to [netlify.com](https://netlify.com) and sign up
2. Drag your project folder to the deploy area OR connect GitHub repo
3. Build command: `npm run build`
4. Publish directory: `dist/public`
5. ✅ Deploy!

### 🟠 GitHub Pages (Static Only)
1. In your repository, go to Settings → Pages
2. Source: "Deploy from a branch"  
3. Branch: `gh-pages` (create this branch first)
4. Add this file as `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [ main ]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '20'
      - run: npm install
      - run: npm run build:client
      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist/public
```

## Step 4: Custom Domain (Optional)

### Buy a domain (like jasonyou.dev):
1. **Namecheap**, **GoDaddy**, or **Google Domains**
2. In your hosting platform (Vercel/Netlify), add your custom domain
3. Update your domain's DNS settings as instructed
4. ✅ SSL certificate is automatic!

## Files Included in Your Package

```
📁 Your Portfolio Website
├── 📄 README.md              # Project documentation
├── 📄 package.json           # Dependencies and scripts
├── 📄 .gitignore            # Git ignore rules
├── 📄 deploy.md             # Detailed deploy guide
├── 📄 DEPLOY_INSTRUCTIONS.md # This quick guide
├── 📁 client/               # Frontend React app
├── 📁 server/               # Backend Express server
├── 📁 shared/               # Shared types
├── 📁 attached_assets/      # Your personal photos
└── 📁 configuration files   # Vite, Tailwind, TypeScript
```

## 🔧 Development Commands

After cloning:
```bash
npm install          # Install dependencies
npm run dev         # Start development server
npm run build       # Build for production
npm run preview     # Preview production build
```

## 📞 Need Help?

1. **Build errors**: Make sure you have Node.js 20+ installed
2. **Images not showing**: Check that your photos are in `attached_assets/`
3. **Contact form**: Backend needed for form functionality (works on Vercel/Netlify)
4. **Domain issues**: DNS changes can take 24-48 hours

## 🎯 What You Get

✅ **Professional portfolio website**  
✅ **Your personal photos integrated**  
✅ **Mobile-responsive design**  
✅ **Working contact form**  
✅ **Berkeley-themed styling**  
✅ **Fast loading and SEO optimized**  
✅ **Easy to update and maintain**  

Your website showcases:
- Your journey from De Anza to UC Berkeley
- InterBridge and your AI education work  
- Bay Area Founders Club involvement
- Experience at Zhencheng Capital & ZhenFund
- Your vision for ethical AI and social impact

**Ready to launch!** 🚀