# One of the approaches to deploy Vite + React app in GitHub

## An easy way to host the application. So far, I have tried with the application which doesn't involve DB)

![Post Image](./resources/post-6-a.webp)

In the application folder, it requires two things.

1\. A change in the existing **vite.config.js file in the main folder**

* `base: "/manage-list-using-local-storage"` as another defineConfig params.
    
* This is the endpoint for the application URL.
    
* The reference is given below.
    
* ### ***<mark>In vite.config.js</mark>*** file
    

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  base: "/home"
})
```

2\. A new file

* In the main folder, create a folder `.github/workflows`
    
* Inside `.github/workflows/`, create `deploy.yml` file.
    
* Reference for the `.yml` content is given below.
    

* ### ***<mark>.github/workflows/deply.yml</mark>*** file
    

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
        uses: actions/checkout@v3
      - name: Set up Node
        uses: actions/setup-node@v3
        with:
          node-version: 18
          cache: 'npm'
      - name: Install dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          # Upload dist repository
          path: './dist'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```

When the code is pushed into the deployment branch (master/main/qa as configured in the GitHub), it automatically starts the build & deploys the application.

The application is running at [https://username.github.io/home/](https://krius2023.github.io/manage-list-using-local-storage/) (endpoint is as mentioned the base value in the vite.config.js file)

I hope, It helps someone or other who is searching for how to deploy vite application in github to host the application.

Thanks for reading. Welcome your comments.
