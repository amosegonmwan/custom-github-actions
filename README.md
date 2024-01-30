# Custom GitHub Actions

This repository showcases different types of custom actions that can be used in GitHub Workflows.

## Types of Custom Actions

### 1. JavaScript Actions

The repository includes examples of JavaScript-based GitHub Actions. These actions are written in JavaScript and can be used to perform specific tasks or automation within your workflows.

**Example Code:**
```javascript
const core = require('@actions/core')
const github = require('@actions/github')
const exec = require('@actions/exec')

function run() {
  core.notice('Hello from my custom JavaScript Action!')
}

run();



# Get & Cache Dependencies Composite Action

This repository contains a GitHub Composite Action named 'Get & Cache Dependencies'. The action is designed to fetch dependencies (via npm) and cache them for improved workflow efficiency.

## Usage

To use this action in your workflow, add the following step to your `.github/workflows/main.yml` file:

```yaml
name: Your Workflow Name

on:
  push:
    branches:
      - main

jobs:
  get-cache-deps-job:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v2

    - name: Get & Cache Dependencies
      uses: ./path/to/get-cache-dependencies
      with:
        caching: true
