# 🚀 Trellis GitHub Deployment

Automatically deploy your [Trellis](https://roots.io/trellis/)-based WordPress site to `staging` and `production` environments on merge to `staging` and `main` branches respectively, and keep plugins, themes, and WordPress core up to date with Dependabot.

## Features

- 🚀 **Automatic (or manual) deployment** to `staging` and `production` environments using [GitHub Actions](https://github.com/features/actions) when pull requests are merged to your `staging` and `main` branches respectively.
- 🔄 **On-Demand sync** database and assets from `production` to `staging`.
- 🔗 **Maintains a history of [GitHub Deployments](https://docs.github.com/en/rest/reference/repos#create-a-deployment)** and provides links to the current deployments in each environment.
- 🔑 **Re-set deployment keys on-demand** when you need to change who has access to `staging` or `production`.
- 📦 **WordPress plugin, core, and theme updates** managed with [Dependabot](https://docs.github.com/en/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically/about-dependabot-version-updates).
- 📝 **Optionally generates README.md** with deployment status badges and setup instructions.

### Optional Additional Workflows
<details>
<summary>Click to expand</summary>

- 🌱 **Sage 10 build test** on pull request or on-demand (make sure your theme builds before you deploy it!).
- 🧪 **Dry-run deployments** to `staging` and `production` environments on pull request or on-demand (confirm Trellis can deploy successfully without finalizing the deployment).
- ⏏️ **Eject WordPress site** from Bedrock and Trellis and prepare database and assets for migration to traditional WordPress hosting.

</details>

---
## Requirements

- A [Trellis](https://roots.io/trellis/docs/installing-trellis/)-based WordPress website.
- Provisioned remote servers for `staging` and `production` environments.

**NOTE**: This project presumes your Trellis-based website and its `staging` and `production` environments are provisioned and deploying successfully.

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

 Automatically deploys to the `production` environment when a `pull_request` is `merged` to the `main` branch. This action can also be run manually from the "Actions" tab in GitHub.

When a deploy to `production` is completed, the following occurs:

- A new release is created with the current date and time including site's database and uploads attached as artifacts (GitHub release size restrictions apply).
- A GitHub Deployment is created with a link to the environment.

</details>

<details>
<summary>🚀 Deploy to staging</summary>
  
```md
.github/workflows/deploy-staging.yml
```

Automatically deploys to the `staging` environment when a `pull_request` is `merged` to the `staging` branch. This action can also be run manually from the "Actions" tab in GitHub.

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
<summary>🔑 Set Trellis deploy keys</summary>

```md
.github/workflows/set-trellis-deploy-keys.yml
```

Updates the ssh keys used by Trellis to deploy to the `staging` or `production` environments. This action can be run manually from the "Actions" tab in GitHub.

This action replaces the current deploy keys with keys with keys defined in one or more of the following locations:

- 'trellis/group_vars/all/users.yml'
- GitHub secrets named `TRELLIS_DEPLOY_KEYS`
- A new key entered manually when running the action

</details>
<details>
<summary>📝 Update README</summary>

```md
.github/workflows/update-readme.yml
```

Updates the README.md with the current deployment status badges. This action can be run manually from the "Actions" tab in GitHub.
</details>
