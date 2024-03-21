# cirrus-os

> Cirrus clouds are often a sign of fair weather, but they can also indicate that a change in weather is on the horizon.

## Goals

The goal of this build is building off of [Bazzite](https://github.com/ublue-os/bazzite) and mix in some of the features of [Bluefin DX](https://github.com/ublue-os/bluefin) to create a **modern** gaming and productivity powerhouse.

## Changes from Bazzite

### Fully implemented
- Docker engine from Docker repos
- Koi (until Plasma 6 comes) - Automatic theme switching
- Gnome-boxes and virt-manager - Virtual Machines
- lightly desktop theme (probably to be removed?)
- solaar for logitech devices
- zerotier and tailscale for connectivity
- 1Password
- A bunch of nerd fonts 🤓

### Wip
- `fastfetch` instead of `neofetch`

### Planned
- `clevis` - for unlocking encrypted partitions with TPM

## Built with BlueBuild

See the [BlueBuild docs](https://blue-build.org/how-to/setup/) for quick setup instructions for setting up your own repository based on this template.


## Installation

> **Warning**  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/flyinpancake/cirrus-os:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/flyinpancake/cirrus-os:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/blue-build/legacy-template
```
