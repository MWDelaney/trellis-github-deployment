# example.com

This [Trellis](https://roots.io/trellis/)-based WordPress project uses GitHub Actions for continuous deployment.

[![Deploy to staging](https://github.com/MWDelaney/example.com/actions/workflows/deploy-staging.yml/badge.svg?branch=staging)](https://github.com/MWDelaney/example.com/actions/workflows/deploy-staging.yml) [![Deploy to production](https://github.com/MWDelaney/example.com/actions/workflows/deploy-production.yml/badge.svg)](https://github.com/MWDelaney/example.com/actions/workflows/deploy-production.yml)

## Deployment

Deployment occurs automatically from this GitHub repository using [GitHub Actions](https://github.com/features/actions).

This project deploys to the `staging` and `production` environments when a `pull_request` is `merged` to `staging` or `main` branches respectively.

GitHub **Deployments** maintain a history of deployments and provide links to the current deployments in each.

[See the current deployments](https://github.com/MWDelaney/example.com/deployments)

<details>
<summary>Initial Setup</summary>

_Note: these instructions presume your `staging` and `production` environments (servers) and DNS are already configured._

### System Requirements

* [Trellis CLI](https://github.com/roots/trellis-cli)
* [Github CLI](https://cli.github.com)

### 1. Create GitHub Secrets

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

### 2. Generate Trellis aliases

From your `site` directory, run:

```bash
trellis alias
```

And update `site/wp-cli.yml` as instructed.

### 3. Grant workflow permissions

 1. In this repository, navigate to `Settings` -> `Actions` -> `General` -> `Workflow Permissions`.
 2. Enable "read and write" permissions.

### 4. Reprovision your environments to allow GitHub's deploy key

Run the following:
  
```bash
trellis provision staging && trellis provision production
```

</details>

## Development

1) Clone this repository locally
2) In the repository directry, run `trellis init`
3) In the repository directory, run `trellis up`
