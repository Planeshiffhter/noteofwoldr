<p align="center">
    <img src="https://docs.goauthentik.io/img/icon_top_brand_colour.svg" height="150" alt="authentik logo">
</p>

---

[![Join Discord](https://img.shields.io/discord/809154715984199690?label=Discord&style=for-the-badge)](https://goauthentik.io/discord)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/Planeshiffhter/noteofwoldr/ci-main.yml?branch=main&label=core%20build&style=for-the-badge)](https://github.com/Planeshiffhter/noteofwoldr/actions/workflows/ci-main.yml)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/Planeshiffhter/noteofwoldr/ci-outpost.yml?branch=main&label=outpost%20build&style=for-the-badge)](https://github.com/Planeshiffhter/noteofwoldr/actions/workflows/ci-outpost.yml)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/Planeshiffhter/noteofwoldr/ci-web.yml?branch=main&label=web%20build&style=for-the-badge)](https://github.com/Planeshiffhter/noteofwoldr/actions/workflows/ci-web.yml)
[![Code Coverage](https://img.shields.io/codecov/c/gh/goauthentik/authentik?style=for-the-badge)](https://codecov.io/gh/goauthentik/authentik)
![Latest version](https://img.shields.io/docker/v/authentik/server?sort=semver&style=for-the-badge)
[![](https://img.shields.io/badge/Help%20translate-transifex-blue?style=for-the-badge)](https://explore.transifex.com/authentik/authentik/)

## What is authentik?

authentik is an open-source Identity Provider (IdP) for modern SSO. It supports SAML, OAuth2/OIDC, LDAP, RADIUS, and more, designed for self-hosting from small labs to large production clusters.

Our [enterprise offering](https://goauthentik.io/pricing) is available for organizations to securely replace existing IdPs such as Okta, Auth0, Entra ID, and Ping Identity for robust, large-scale identity management.

## Installation

- Docker Compose: recommended for small/test setups. See the [documentation](https://docs.goauthentik.io/docs/install-config/install/docker-compose/).
- Kubernetes (Helm Chart): recommended for larger setups. See the [documentation](https://docs.goauthentik.io/docs/install-config/install/kubernetes/) and the Helm chart [repository](https://github.com/goauthentik/helm).
- AWS CloudFormation: deploy on AWS using our official templates. See the [documentation](https://docs.goauthentik.io/docs/install-config/install/aws/).
- DigitalOcean Marketplace: one-click deployment via the official Marketplace app. See the [app listing](https://marketplace.digitalocean.com/apps/authentik).

### Build the standalone snapshot locally

On Windows, enable Docker Desktop's WSL 2 integration and run these commands from your WSL distribution.

```shell
git clone https://github.com/Planeshiffhter/noteofwoldr.git
cd noteofwoldr
```

Create a `.env` file in the checkout and use a different value from `openssl rand -hex 48` for each secret.

```dotenv
AUTHENTIK_SECRET_KEY=replace-with-a-generated-secret
AUTHENTIK_POSTGRESQL__PASSWORD=replace-with-a-generated-password
```

The bundled PostgreSQL service uses `postgresql` as its hostname and `authentik` as its database and user. You can override these with `AUTHENTIK_POSTGRESQL__HOST`, `AUTHENTIK_POSTGRESQL__NAME`, and `AUTHENTIK_POSTGRESQL__USER`. The Compose file disables error reporting, startup analytics, and update checks by default.

```shell
docker compose -f docker-compose.local.yml up --build -d
```

Open <http://localhost:9000/if/flow/initial-setup/> to initialize the installation. The server and worker share an image built from `lifecycle/container/Dockerfile`. Its build uses the upstream `fips-debian`, `fips-python`, and `geoip` images.

Configure `AUTHENTIK_EMAIL__*` in `.env` if you need email. For separate outposts, set `AUTHENTIK_OUTPOSTS__CONTAINER_IMAGE_BASE` to your outpost image template, such as `registry.example.com/authentik/%(type)s:%(version)s`. The worker in this Compose file runs without a host Docker socket, so use a separate Docker integration or deploy external outposts manually.

## Screenshots

| Light                                                       | Dark                                                       |
| ----------------------------------------------------------- | ---------------------------------------------------------- |
| ![](https://docs.goauthentik.io/img/screen_apps_light.jpg)  | ![](https://docs.goauthentik.io/img/screen_apps_dark.jpg)  |
| ![](https://docs.goauthentik.io/img/screen_admin_light.jpg) | ![](https://docs.goauthentik.io/img/screen_admin_dark.jpg) |

## Development and contributions

See the [Developer Documentation](https://docs.goauthentik.io/docs/developer-docs/) for information about setting up local build environments, testing your contributions, and our contribution process.

When you contribute documentation, either to accompany a code change or as a standalone contribution, please be sure to follow our documentation [Style Guide](website/docs/developer-docs/docs/style-guide.mdx).

## Security

Please see [SECURITY.md](SECURITY.md).

## Adoption

Using authentik? We'd love to hear your story and feature your logo. Email us at [hello@goauthentik.io](mailto:hello@goauthentik.io) or open a GitHub Issue/PR!

## License

[![MIT License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey?style=for-the-badge)](website/LICENSE)
[![authentik EE License](https://img.shields.io/badge/License-EE-orange?style=for-the-badge)](authentik/enterprise/LICENSE)
