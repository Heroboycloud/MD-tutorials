# Learning GitHub Actions: Examples and Concepts

GitHub Actions is a powerful automation tool that lets you build, test, and deploy your code right from GitHub. Here's a comprehensive guide with practical examples to help you master it.

## Core Concepts

1. **Workflows**: Automated processes defined in YAML files in `.github/workflows/`
2. **Events**: Triggers that start workflows (pushes, PRs, schedules, etc.)
3. **Jobs**: Groups of steps that run on the same runner
4. **Steps**: Individual tasks that can run commands or actions
5. **Actions**: Reusable units of code that perform specific tasks

## Basic Example: CI Pipeline

```yaml
name: CI Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '20'
        
    - name: Install dependencies
      run: npm install
      
    - name: Run tests
      run: npm test
```

## Intermediate Examples

### 1. Scheduled Job

```yaml
name: Daily Backup

on:
  schedule:
    - cron: '0 0 * * *'  # Runs at midnight UTC every day

jobs:
  backup:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: ./scripts/backup.sh
```

### 2. Matrix Testing (Multiple Versions)

```yaml
name: Test Matrix

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [14.x, 16.x, 18.x, 20.x]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm install
      - run: npm test
```

### 3. Deployment to AWS S3

```yaml
name: Deploy to S3

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
      - name: Deploy to S3
        run: aws s3 sync ./dist s3://your-bucket-name --delete
```

## Advanced Examples

### 1. Docker Build and Push

```yaml
name: Docker Build and Push

on:
  push:
    tags:
      - 'v*'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_HUB_USERNAME }}
          password: ${{ secrets.DOCKER_HUB_TOKEN }}
          
      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: user/app:latest,user/app:${{ github.ref_name }}
```

### 2. Self-hosted Runner with Custom Hardware

```yaml
name: GPU Tests

on: [push]

jobs:
  test:
    runs-on: [self-hosted, gpu]
    steps:
      - uses: actions/checkout@v4
      - name: Install CUDA
        run: |
          sudo apt-get update
          sudo apt-get install -y nvidia-cuda-toolkit
      - name: Run GPU tests
        run: ./run-gpu-tests.sh
```

### 3. Slack Notifications

```yaml
name: Build Notification

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install && npm run build
      
  notify