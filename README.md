# Continuous Deployment for Trellis using GitHub Actions

A basic set of Github workflows to perform the following Trellis chores and DevOps tasks:

* Automate pull-requests for WordPress plugin and core updates with Dependabot
* Automate deployment to staging and production environments

## Setting up This Repository for the First Time

1) Clone this repository locally
2) Run `trellis new example.com && trellis key generate && trellis vault encrypt && mv README.md README.template.md && mv README.trellis-template.md README.md`
3) Document the new keys, document the `trellis/.vault_pass` file, commit the new files.
