# vite-react-gh-pages
*Guide to deploy vite react app to github pages*

## create repo

![image](images/1.jpg)

## clone repo (github desktop)

![image](images/2.jpg)

## install vite

```bash
npm install vite@latest 
```

![image](images/3.jpg)
![image](images/4.jpg)
![image](images/5.jpg)

## move files to root folder

![image](images/6.jpg)
![image](images/7.jpg)

## change vite.config.js


on **vite.config.js** change the base name to the repo name
example: ```base: '/<REPO>/' ```

mine:
```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  base: '/vite-react-gh-pages/' // Set the base path for GitHub Pages deployment
})
```
![image](images/8.jpg)

## add github workflow deploy file

create **.github/workflows/deploy.yml** with the following content:
```yaml
# Simple workflow for deploying static content to GitHub Pages
name: Deploy static content to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ['main']

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets the GITHUB_TOKEN permissions to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow one concurrent deployment
concurrency:
  group: 'pages'
  cancel-in-progress: true

jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5
      - name: Set up Node
        uses: actions/setup-node@v5
        with:
          node-version: lts/*
          cache: 'npm'
      - name: Install dependencies
        run: npm ci
      - name: Build
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v4
        with:
          # Upload dist folder
          path: './dist'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

```

![image](images/9.jpg)

## change settings => pages => source to gh actions

![image](images/13.jpg)

## commit and push all changes
![image](images/10.jpg)
![image](images/11.jpg)

## wait for gh actions to finish

![image](images/15.jpg)
![image](images/16.jpg)

## visit deployed site

https://joeyvigil.github.io/vite-react-gh-pages/

![image](images/14.jpg)

## sources
https://vite.dev/guide/static-deploy.html#github-pages
