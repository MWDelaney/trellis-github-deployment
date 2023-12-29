# 🚀 Trellis GitHub Deployment

Automatically deploy your [Trellis](https://roots.io/trellis/)-based WordPress site to `staging` and `production` environments on merge to `staging` and `main` branches respectively, and keep plugins, themes, and WordPress core up to date with Dependabot.

🔥 Based on [setup-trellis-cli](https://github.com/roots/setup-trellis-cli). This set of GitHub actions and workflows extend the functionality of that package to more tightly integrate with GitHub's native features.

> [!IMPORTANT]  
> When upgrading from version 1.x to 2.x, you must update your GitHub secrets to remove the `TRELLIS_SITE_SLUG` secret and confirm that your repository is named after your trellis site slug. For example, if your site slug is `example.com`, your repository must be named `example.com`, per Roots' best practice.

## Features

- 🚀 **Automatic (or manual) deployment** to `staging` and `production` environments using [GitHub Actions](https://github.com/features/actions) when pull requests are merged to your `staging` and `main` branches respectively.
- 🔄 **On-Demand one-way sync** database and assets from `production` to `staging`.
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
- ⛵ **Unlighthouse Audit Production** on-demand (or on a schedule) to audit your production site's performance using [Unlighthouse](https://unlighthouse.dev) and publish the results as a GitHub Pages site.
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

### Default Workflows

These workflows are included and enabled by default.

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

- `trellis/group_vars/all/users.yml`
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

### Optional Workflows

These example workflows are included to expand the functionality of this project. They are not enabled by default.

<details>
<summary>🧪 Dry-Run to Production</summary>

```md
.github/examples/dryrun-production.yml
```

⚠️ **NOTE:** This workflow must be moved to the `.github/workflows` directory to be used.

Performs a "dry-run" deployment to the `production` environment, testing all aspects of a Trellis deployment without finalizing the deploy. Automatically deploys to the `staging` environment when a `pull_request` is `opened` to the `main` branch. This action can also be run manually from the "Actions" tab in GitHub.
</details>
<details>
<summary>🧪 Dry-Run to Staging</summary>

```md
.github/examples/dryrun-staging.yml
```

⚠️ **NOTE:** This workflow must be moved to the `.github/workflows` directory to be used. 

Performs a "dry-run" deployment to the `staging` environment, testing all aspects of a Trellis deployment without finalizing the deploy. Automatically deploys to the `staging` environment when a `pull_request` is `opened` to the `staging` branch. This action can also be run manually from the "Actions" tab in GitHub.
</details>
<details>
<summary>🌱 Sage 10 Build Test</summary>

```md
.github/examples/sage10-build-test.yml
```

⚠️ **NOTE:** This workflow must be moved to the `.github/workflows` directory to be used.

⚠️ **NOTE:** You must edit this workflow to update the `theme_slug` variable with your theme's slug.

Builds the Sage 10 theme and runs the theme's tests. Automatically runs when a `push` is made to any branch.
</details>
<details>
<summary>⏏️ Eject Production</summary>

```md
.github/examples/eject-production.yml
```

⚠️ **NOTE:** This workflow must be moved to the `.github/workflows` directory to be used.

Exports a WordPress site built with Trellis from the `production` environment for delivery to a traditional WordPress environment and attach artifacts to the workflow run for download.  This action can be run manually from the "Actions" tab in GitHub.
</details>

### Dependabot

<details>
<summary>🤖 WordPress core, plugin, and theme updates</summary>

Dependabot will check for updates to WordPress themes, plugins, and core as defined in `site/composer.json` on a weekly basis and propose updates as pull requests to the `staging` branch. You can change this behavior by editing the `.github/dependabot.yml` file.
</details>
