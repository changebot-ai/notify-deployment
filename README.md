# Changebot Notify Deployment Action

A GitHub Action that automatically notifies [Changebot](https://changebot.ai) of deployment events.

Changebot is a product enablement automation platform that automatically generates customer-facing product updates directly from your development workflow.

## Quick Start

**Step 1**: Add permissions to your workflow job:

```yaml
permissions:
  id-token: write
  contents: read
```

**Step 2**: Add the action to your workflow:

```yaml
- uses: changebot-ai/notify-deployment@v1
```

## Usage

### Basic Usage

```yaml
name: Deploy and Notify
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest

    permissions:
      id-token: write
      contents: read

    steps:
      - uses: actions/checkout@v5

      - name: Deploy application
        run: echo "Deploying application..."

      - name: Notify Changebot
        uses: changebot-ai/notify-deployment@v1
```

### Staging Environment

```yaml
- uses: changebot-ai/notify-deployment@v1
  with:
    environment: "staging"
```

## Inputs

| Input         | Description               | Required | Default      |
| ------------- | ------------------------- | -------- | ------------ |
| `environment` | `production` or `staging` | No       | `production` |

## Prerequisites

1. Sign up at [changebot.ai](https://changebot.ai)
2. Install the Changebot GitHub App on your organization
3. Ensure your repository is connected to Changebot

## How It Works

Uses GitHub's OIDC to authenticate with Changebot without API keys:

1. GitHub generates a short-lived JWT token
2. Action sends deployment details to Changebot
3. Changebot verifies the JWT and processes the deployment

## Troubleshooting

**"OIDC token unavailable" error**: Add `permissions: id-token: write` to your workflow job

**Invalid environment error**: Use exactly `production` or `staging` (case-sensitive)

**JWT verification failed**: Ensure Changebot GitHub App is installed on your repository

## Support

🐛 **Issues**: [GitHub Issues](https://github.com/changebot-ai/notify-deployment/issues)
