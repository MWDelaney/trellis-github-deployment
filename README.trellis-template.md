# example.com

[![Deploy to staging](https://github.com/RebelInteractiveGroup/trellis-template/actions/workflows/deploy-staging.yml/badge.svg?branch=staging)](https://github.com/RebelInteractiveGroup/trellis-template/actions/workflows/deploy-staging.yml)

[![Deploy to production](https://github.com/RebelInteractiveGroup/trellis-template/actions/workflows/deploy-production.yml/badge.svg)](https://github.com/RebelInteractiveGroup/trellis-template/actions/workflows/deploy-production.yml)

## System Requirements

* [Trellis CLI](https://github.com/roots/trellis-cli)

<details>
  <summary>Initial Setup</summary>

## Setting up This Repository for the First Time

1) Clone this repository locally
2) Run `trellis new example.com && trellis key generate && trellis vault encrypt && mv README.md README.template.md && mv README.trellis-template.md README.md`
3) Document the new keys, document the `trellis/.vault_pass` file, commit the new files.

</details>

---
## Development

1) Clone this repository locally
2) In the repository directry, run `trellis init`
3) In the repository directory, run `trellis up`
