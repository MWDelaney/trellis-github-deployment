# Continuous Deployment for Trellis using GitHub Actions

A basic set of Github workflows to perform the following Trellis chores and DevOps tasks:

* Automate pull-requests for WordPress plugin and core updates with Dependabot
* Automate deployment to staging and production environments

## System Requirements

* [Trellis CLI](https://github.com/roots/trellis-cli)
* [GitHub CLI](https://cli.github.com)

## Setting up This Repository for the First Time

1) Clone this repository locally
2) Run `trellis new . --force trellis vault encrypt && gh secret set ANSIBLE_VAULT_PASSWORD -b $(cat trellis/.vault_pass) && rm -f README.md && cp .github/README.trellis-template.md README.md`
3) Create, provision staging and production servers, DNS entries, update `trellis/hosts` entries
4) Run `trellis key generate` 
5) Document the new keys, document the `trellis/.vault_pass` file, commit the new files.
