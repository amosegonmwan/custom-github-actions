# Deploy to AWS S3 GitHub Action

This repository contains a GitHub Action for deploying a static website via AWS S3.

## Usage

To use this action in your workflow, add the following step to your `.github/workflows/main.yml` file:

```yaml
name: Deploy to AWS S3

on:
  push:
    branches:
      - main

jobs:
  deploy-job:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v2

    - name: Deploy to AWS S3
      uses: your-username/your-repo-name@v1
