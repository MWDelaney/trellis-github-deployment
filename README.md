# trellis-template

This [Trellis](https://roots.io/trellis/)-based WordPress project uses GitHub Actions for continuous deployment.

[![Deploy to staging](https://github.com/MWDelaney/trellis-template/actions/workflows/deploy-staging.yml/badge.svg?branch=staging)](https://github.com/MWDelaney/trellis-template/actions/workflows/deploy-staging.yml) [![Deploy to production](https://github.com/MWDelaney/trellis-template/actions/workflows/deploy-production.yml/badge.svg)](https://github.com/MWDelaney/trellis-template/actions/workflows/deploy-production.yml)

## Deployment

Deployment occurs automatically from this GitHub repository using [GitHub Actions](https://github.com/features/actions).

This project deploys to the `staging` and `production` environments when a `pull_request` is `merged` to `staging` or `main` branches respectively.

GitHub **Deployments** maintain a history of deployments and provide links to the current deployments in each.

[See the current deployments](https://github.com/MWDelaney/trellis-template/deployments)

<details>
<summary>Initial Setup</summary>

_Note: these instructions presume your `staging` and `production` environments (servers) and DNS are already configured._

### System Requirements

* [Trellis CLI](https://github.com/roots/trellis-cli)
* [Github CLI](https://cli.github.com)

### 1. Create a new Trellis project in this repository

```bash
trellis new --force .
```

### 2. Update Trellis config for your project

* Update your new Trellis project's [wordpress_sites.yml files](https://roots.io/trellis/docs/wordpress-sites/)
* Update your new Trellis project's `hosts` files
* (Optional) If your project uses private composer repositories, add [Composer authentications](https://roots.io/trellis/docs/composer-http-basic-authentication/) to your new Trellis project's `vault.yml` files.
* **IMPORTANT**: Run `trellis vault encrypt` to encrypt your project's vaults.
* Run `trellis alias` update `site/wp-cli.yml` as instructed.

### 3. Create GitHub Secrets

Deployment relies on 4 GitHub secrets:

Modify and run the following to generate these secrets:

```bash
trellis key generate && gh secret set ANSIBLE_VAULT_PASSWORD -b $(cat trellis/.vault_pass) && gh secret set TRELLIS_SITE_SLUG -b example.com
```

#### Secrets

* `TRELLIS_DEPLOY_SSH_PRIVATE_KEY` - A private key used by GitHub to connect to your environments.
* `TRELLIS_DEPLOY_SSH_KNOWN_HOSTS` - `known_hosts` keys for your environments.
* `ANSIBLE_VAULT_PASSWORD` - Your new Trellis project's [vault password](https://roots.io/trellis/docs/vault/).
* `TRELLIS_SITE_SLUG` - The slug from your new Trellis project's `wordpress_sites.yml` file.

### 4. Grant workflow permissions

 1. In this repository, navigate to `Settings` -> `Actions` -> `General` -> `Workflow Permissions`.
 2. Enable "read and write" permissions.

### 5. Provision your environments

Modify and run tun the following to provision your `staging` and `production` environments:

```bash
git add . && git commit -m "🎉 Initial commit" && git push && trellis provision staging && trellis provision production && git checkout -b staging && git push --set-upstream origin staging && git checkout main && && trellis deploy staging && trellis deploy production && cd site && wp @staging core install --url=example.com --title="Example" --admin_user=admin --admin_email=admin@example.com && wp @production core install --url=example.com --title="Example" --admin_user=admin --admin_email=admin@example.com && cd ..
```

</details>

## Development

1) Clone this repository locally
2) In the repository directry, run `trellis init`
3) In the repository directory, run `trellis up`
