# 🚀 GitHub Setup & Deployment Guide

Follow these steps to publish your birthday website on GitHub!

---

## Step 1: Create a GitHub Repository

1. Go to [GitHub](https://github.com) and sign in to your account
2. Click the **"+"** button in the top right corner
3. Select **"New repository"**
4. Name your repository (e.g., `birthday-website` or `happy-birthday-love`)
5. Choose **"Public"** (so GitHub Pages can work)
6. Click **"Create repository"**

---

## Step 2: Upload Your Files

### Option A: Using GitHub Web Interface (Easiest)

1. On your new repository page, click **"uploading an existing file"**
2. Drag and drop ALL files from the `app` folder:
   - `index.html`
   - `package.json`
   - `tsconfig.json`
   - `tailwind.config.js`
   - `vite.config.ts`
   - `postcss.config.js`
   - `components.json`
   - `src/` folder (with all files inside)
   - `public/` folder (if exists)
3. Click **"Commit changes"**

### Option B: Using Git Command Line

```bash
# Navigate to your project folder
cd /path/to/your/app

# Initialize git
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit - Birthday website"

# Connect to GitHub (replace with your repo URL)
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# Push to GitHub
git branch -M main
git push -u origin main
```

---

## Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **"Settings"** tab
3. Scroll down to **"Pages"** section (or click "Pages" in the left sidebar)
4. Under **"Source"**, select **"Deploy from a branch"**
5. Select **"main"** branch and **"/ (root)"** folder
6. Click **"Save"**

Wait 1-2 minutes for the site to deploy!

---

## Step 4: Add Your Song File

The song file is too large for GitHub's web interface. You'll need to use Git LFS or upload it via command line:

### Using Git Command Line:

```bash
# Navigate to your project
cd /path/to/your/app

# Copy your song to the public folder
cp "albumatycomhamobekaamotana_nzCulz12 ggg.mp3" public/birthday-song.mp3

# Add and commit
git add public/birthday-song.mp3
git commit -m "Add birthday song"
git push
```

---

## Step 5: Build and Deploy

GitHub Pages needs the built files. You have two options:

### Option A: Build Locally and Push dist folder

```bash
# Install dependencies
npm install

# Build the project
npm run build

# Add dist folder to git
git add dist -f
git commit -m "Add build files"
git push

# Then in GitHub Pages settings, select "main" branch and "/dist" folder
```

### Option B: Use GitHub Actions (Auto-deploy)

Create a file `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Build
        run: npm run build
      
      - name: Setup Pages
        uses: actions/configure-pages@v4
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: './dist'
      
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

---

## 🎉 Your Website is Live!

After setup, your website will be available at:

```
https://YOUR_USERNAME.github.io/YOUR_REPO_NAME
```

---

## 💡 Tips

- The "No" button in the Yes/No question moves away when hovered - it's a fun prank!
- The confetti effect triggers when clicking the Surprise button
- You can customize the message in `src/App.tsx`
- The song plays when clicking "Play Your Song" in the Surprise modal

---

## 🆘 Need Help?

If you get stuck:
1. Check GitHub's [Pages documentation](https://docs.github.com/en/pages)
2. Make sure your repository is public
3. Verify the build completed successfully

---

**Made with 💕 for the most special person in your life!**
