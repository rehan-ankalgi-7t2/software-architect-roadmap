GitHub Actions - Detailed Guide

GitHub Actions is a CI/CD (Continuous Integration and Continuous Deployment) service built into GitHub. It enables developers to automate software workflows, including testing, building, and deployment.


---

1. Key Concepts in GitHub Actions

1.1. Workflows

A workflow is an automated process that runs one or more jobs. It is defined in a YAML file inside the .github/workflows/ directory of your repository.

Workflows run in response to GitHub events like push, pull_request, or on a schedule.


1.2. Events

Workflows are triggered by events such as:

push → Runs when a commit is pushed.

pull_request → Runs when a PR is created or updated.

schedule → Runs at a specified time (like a cron job).

workflow_dispatch → Manually triggered workflow.


1.3. Jobs

A job is a set of steps that run on a GitHub-hosted runner (like Ubuntu, macOS, Windows).

Jobs run in parallel by default but can be made dependent on each other.


1.4. Steps

A step is an individual task inside a job. Steps execute commands or run predefined actions.

1.5. Actions

An action is a reusable unit of code (like a plugin). It can be used to run scripts, install dependencies, deploy applications, etc.

Example: actions/checkout@v4 checks out the repo before running other steps.


1.6. Runners

A runner is a virtual machine where the workflow runs. GitHub provides hosted runners (Ubuntu, Windows, macOS), but you can also use self-hosted runners.


---

2. Basic GitHub Actions Workflow Example

Create a .github/workflows/ci.yml file in your repository:

name: CI Pipeline

on: 
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

Explanation:

1. Triggers on push and pull_request to main.


2. Runs a job (build) on Ubuntu.


3. Steps:

Checks out the repository (actions/checkout).

Sets up Node.js 18 (actions/setup-node).

Installs dependencies (npm install).

Runs tests (npm test).





---

3. Advanced GitHub Actions Concepts

3.1. Using Matrix Builds (Run on Multiple Environments)

You can test your code on different OS versions and Node.js versions.

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [16, 18, 20]
        os: [ubuntu-latest, windows-latest]

    steps:
      - uses: actions/checkout@v4
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm install
      - run: npm test

3.2. Using Secrets & Environment Variables

You can store API keys and sensitive information as secrets in GitHub Settings → Secrets and Variables.

env:
  DATABASE_URL: ${{ secrets.DATABASE_URL }}

steps:
  - name: Print Environment Variable
    run: echo "Database URL is $DATABASE_URL"

3.3. Deploying to AWS S3 (Example Deployment Workflow)

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v4

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Deploy to S3
        run: aws s3 sync ./build s3://my-bucket-name --delete


---

4. Reusable Workflows & Composite Actions

4.1. Creating a Reusable Workflow

A reusable workflow can be called from other workflows.

ci.yml (Reusable workflow)

name: Reusable CI Workflow

on: 
  workflow_call:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install
      - run: npm test

deploy.yml (Calls the reusable workflow)

jobs:
  call-workflow:
    uses: my-org/my-repo/.github/workflows/ci.yml@main

4.2. Creating a Composite Action

A composite action is a custom reusable action stored in your repo.

Create .github/actions/setup-node/action.yml:

name: Setup Node.js
description: Install Node.js and dependencies
runs:
  using: "composite"
  steps:
    - uses: actions/setup-node@v4
      with:
        node-version: 18
    - run: npm install
      shell: bash

Use it in your workflow:

steps:
  - uses: ./.github/actions/setup-node


---

5. Monitoring & Debugging Workflows

5.1. Checking Workflow Logs

Go to the GitHub repository → Click Actions → Select the workflow → View logs.


5.2. Debugging Failures

Add debugging logs with echo or env variables.

Use set -x in shell scripts for detailed logging.

Enable GitHub Actions Debug Mode:

Go to Settings → Secrets and Variables → Variables.

Add ACTIONS_STEP_DEBUG = true.




---

6. Optimizing Workflows for Performance

6.1. Caching Dependencies

To speed up installs, cache dependencies like node_modules.

steps:
  - uses: actions/cache@v3
    with:
      path: ~/.npm
      key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
      restore-keys: ${{ runner.os }}-node-

6.2. Running Jobs in Parallel

By default, jobs run in parallel, reducing execution time.

6.3. Using Self-Hosted Runners

For faster builds, use self-hosted runners instead of GitHub-hosted VMs.


---

7. Conclusion

GitHub Actions is a powerful CI/CD tool that helps automate testing, building, and deployment. You can:
✅ Automate testing with multiple environments.
✅ Deploy applications to AWS, Firebase, or Docker.
✅ Secure secrets with GitHub Secrets.
✅ Optimize performance using caching and parallel jobs.

Would you like help setting up GitHub Actions for a specific project?