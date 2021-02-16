## Vue-pipeline

This repository contains a simple **Github Actions Pipeline** to build and deploy Vue app. When `main` branch receives a push, the pipeline is triggered, setting up and building the application. The resulting `dist` directory is pushed to `stage` branch.

### Workflow
`./github/workflows/build.yml`
```
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2
        
      - name: Install dependencies
        run: npm install
        
      - name: Build
        run: npm run build

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          publish_branch: stage
          allow_empty_commit: true
```
