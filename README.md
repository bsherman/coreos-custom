# ucore-main

[![build-ucore](https://github.com/bsherman/ucore-main/actions/workflows/build.yml/badge.svg)](https://github.com/bsherman/ucore-main/actions/workflows/build.yml)

## WARNING: STOP USING ME

Builds will continue to be generated but all development efforts for uCore have moved to:

https://github.com/ublue-os/ucore



## What is this?

This is an OCI image of [Fedora CoreOS](https://getfedora.org/coreos/) with quality of life improvments.

### WARNING: not yet tested

## Features

- Start with Fedora CoreOS image
- add some packages:
  - cockpit
  - distrobox
  - docker-compose & podman-compose
  - duperemove
  - tailscale and wireguard-tools
- remove some packages:
  - toolbox
  - zincati
- Sets automatic staging of updates for system
- 60 second service stop timeout for reasonably fast shutdowns

This image should be suitable for use on bare metal or in a virtual machines where you wish to run containerized workloads. It uses sign
ificantly less disk space than [ucore-hci](https://github.com/bsherman/ucore-hci), but check that out if you need to host virtual machines or run ZFS.

One can also layer packages directly on a machine running this or use this image as a base for a further customized OCI.

Note: cockpit-ws runs as a podman container, not a direct systemd service. This image pre-configures it to run, but it can be disabled:

    sudo systemctl disable --now cockpit.service


## Usage

To rebase an Fedora CoreOS machine to the latest release (stable):

    sudo rpm-ostree rebase ostree-unverified-registry:ghcr.io/bsherman/ucore-main:stable

  
## Verification

These images are signed with sisgstore's [cosign](https://docs.sigstore.dev/cosign/overview/). You can verify the signature by downloading the `cosign.pub` key from this repo and running the following command:

    cosign verify --key cosign.pub ghcr.io/bsherman/ucore-main
