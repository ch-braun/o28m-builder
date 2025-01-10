# Open-Telekom-Integration-Platform (O28M) Builder

This repository contains suggestions for build scripts for
the [Open-Telekom-Integration-Platform](https://github.com/telekom/Open-Telekom-Integration-Platform) (O28M) components.

The steps included are:

- Pulling the needed repositories
- Building the images
- Pushing them to a registry

The workflows are bundled per component and can be found in the `.github/workflows` directory.

## Components and Images

- [x] [Identity-Iris](.github/workflows/identity-iris.yml):
    - [x] Identity-Iris-Keycloak (A modified Keycloak image)
- [x] [Gateway](.github/workflows/gateway.yml):
    - [x] Gateway-Kong (A Kong image with jwt-keycloak plugin)
    - [x] Gateway-Jumper (A sidecar container for the Gateway)
    - [x] Gateway-Issuer-Service (A sidecar container for the Gateway)
    - [x] Gateway-Bash-Curl (A helper image to bootstrap and configure the Gateway)

## Usage

To use the build scripts for your own purposes, it is recommended to fork this repository and adjust the workflows to
your needs.

Parameters that can be adjusted are:

| Parameter                  | Description                                        | Default       | Required | Example                                                        |
|----------------------------|----------------------------------------------------|---------------|----------|----------------------------------------------------------------|
| `source_repository`        | The repository to pull the source code from        | `''`          | Yes      | `telekom/gateway-jumper`                                       |
| `source_branch`            | The branch to pull the source code from            | `main`        | Yes      | `main`                                                         |
| `source_dockerfile`        | The path to the Dockerfile                         | `Dockerfile`  | No       | `Dockerfile`                                                   |
| `source_build_context`     | The context to build the image from                | `.`           | No       | `.`                                                            |
| `target_image`             | The name of the image to build                     | `''`          | Yes      | `ghcr.io/${{ github.repository_owner }}/gateway-jumper:latest` |
| `target_architecture`      | The platforms/architectures to build the image for | `linux/amd64` | No       | `linux/amd64,linux/arm64`                                      |
| `target_registry`          | The registry to push the image to                  | `''`          | No       | `ghcr.io`                                                      |
| `target_registry_username` | The username to authenticate with the registry     | `''`          | No       | `${{ github.actor }}`                                          |
| `target_registry_password` | The password to authenticate with the registry     | `''`          | No       | `${{ secrets.GITHUB_TOKEN }}`                                  |

## License

This repository is licensed under the Apache 2.0 License. See the [LICENSE](LICENSE) file for more information.
