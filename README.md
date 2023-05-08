# 🚀 Trellis GitHub Deployment

Automatically deploy [Trellis](https://roots.io/trellis/)-based WordPress site to `staging` and `production` environments on merge to `staging` and `main` branches respectively, and keep plugins, themes, and WordPress core up to date with Dependabot.

## Features

- 🚀 **Automatic deployment** to `staging` and `production` environments using [GitHub Actions](https://github.com/features/actions).
- 🔄 **On-Demand sync** database and assets from `production` to `staging`.
- 🔗 **Maintains a history of [GitHub Deployments](https://docs.github.com/en/rest/reference/repos#create-a-deployment)** and provides links to the current deployments in each environment.
- 📦 **WordPress plugin, core, and theme updates** managed with [Dependabot](https://docs.github.com/en/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically/about-dependabot-version-updates).
- 📝 **Automatically updates README.md** with deployment status badges.

### Optional Additional Workflows
<details>
<summary>Click to expand</summary>

- 🌱 Sage 10 asset building on pull request or on-demand (make sure your theme builds before you deploy it!).
- 🧪 Dry-run deployments to `staging` and `production` environments on pull request or on-demand (confirm Trellis can deploy successfully without finalizing the deployment).
- ⏏️ Eject WordPress site from Bedrock and Trellis and prepare database and assets for migration to traditional WordPress hosting.

</details>

---
## Requirements

- A [Trellis](https://roots.io/trellis/docs/installing-trellis/)-based WordPress website.
- Provisioned remote servers for `staging` and `production` environments.

## Installation

1. Copy the `.github` directory from this repository to your Trellis-based WordPress site's repository.
2. Refer to the Initial Setup instructions in `.github/README.md` to configure your GitHub repository for deployment.

---

## Usage

<details>
<summary>🚀 Deploy to production</summary>

```md
.github/workflows/deploy-production.yml
```

 Automatically deploys to the `production` environment when a `pull_request` is `merged` to the `main` branch.

When a deploy to `production` is completed, the following occurs:

- A new release is created with the current date and time including site's database and assets attached as artifacts.
- A GitHub Deployment is created with a link to the environment.

</details>

<details>
<summary>🚀 Deploy to staging</summary>
  
```md
.github/workflows/deploy-staging.yml
```

Automatically deploys to the `staging` environment when a `pull_request` is `merged` to the `staging` branch.

When a deploy to `staging` is completed, the following occurs:

- A new tag is created with the current date and time.
- A GitHub Deployment is created with a link to the environment.

</details>

<details>
<summary>🔄 Sync content production->staging</summary>

```md
.github/workflows/sync-content-production-to-staging.yml
```

Copy the database and assets from the `production` environment to the `staging` environment overwriting the staging environment's database and assets.

</details>

<details>
<summary>📝 Update README</summary>

```md
.github/workflows/update-readme.yml
```

Updates the README.md with the current deployment status badges.
