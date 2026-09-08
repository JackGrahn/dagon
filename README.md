# dagon &nbsp; [![bluebuild build badge](https://github.com/jackgrahn/dagon/actions/workflows/build.yml/badge.svg)](https://github.com/jackgrahn/dagon/actions/workflows/build.yml)

Dagon is my personal KDE developer image, built with [BlueBuild](https://blue-build.org/) on top of [Universal Blue](https://universal-blue.org/)'s Kinoite. It ships with VS Code, Brave Origin, podman, the GitHub CLI and Homebrew (included in the Kinoite base), with full media codecs and personal configuration applied via [chezmoi](https://www.chezmoi.io/).

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/jackgrahn/dagon:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/jackgrahn/dagon:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/how-to/generate-iso/#_top). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/jackgrahn/dagon
```
