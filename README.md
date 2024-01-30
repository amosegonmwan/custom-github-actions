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
```

### 2. Composite Actions
GitHub Composite Actions provide a way to encapsulate multiple steps into a reusable and shareable action. Unlike regular actions that are defined in a single repository, composite actions can be composed of multiple steps from different repositories. This allows for more modular and maintainable workflows.


```yaml
name: 'Get & Chache Dependencies'
description: 'Get the dependencies (via npm) and chache them.'
inputs:
  caching:
    description: 'Whether to chache dependencies or not.'
    required: false
    default: 'true'
outputs:
  used-cache:
    description: 'Whether the chache was used.'
    value: ${{ steps.install.outputs.cache }}
runs:
  using: 'composite'
  steps:
    - name: Cache dependencies
      if: inputs.caching == 'true'
      id: cache
      uses: actions/cache@v3
      with:
        path: node_modules
        key: deps-node-modules-${{ hashFiles('**/package-lock.json') }}
    - name: Install dependencies
      if: steps.cache.outputs.cache-hit != 'true' || inputs.caching != 'true'
      run: |
        npm ci
        echo "::set-output name=cache:: '${{ inputs.caching }}' "
      shell: bash
```

### Usage Notes:
* In the workflow definition, specify the path to the 'Get & Cache Dependencies' composite action.
* Customize the with section to set input parameters according to your requirements.
* The caching input parameter is optional and has a default value of true. You can override it as needed.
* The output used-cache can be accessed in subsequent steps or jobs. In this example, it is set to the value of the 'cache' output from the 'Install dependencies' step.
* Adjust the workflow and action paths based on your project structure. 


### 3. Docker Actions
Docker actions provide a way to encapsulate and execute steps within a Docker container in a GitHub workflow. These actions are especially useful when you want to ensure a consistent and reproducible environment for your tasks.
