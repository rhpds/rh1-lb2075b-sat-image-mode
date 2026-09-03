# Module Outline: module-06-update-image

## Brief Overview

This module moves to rhel1, the builder node, where participants customize a bootc container image. They write a Containerfile that extends the official `registry.redhat.io/rhel10/rhel-bootc:10.1` base image with a custom message-of-the-day (MOTD) featuring an ASCII happy face, then build the image with Podman and apply a tag that matches the Satellite container registry path. The base image is pre-pulled on rhel1, so no external network access is required during the build.

## Audience and Time

- **Target personas:** Systems administrators, platform engineers
- **Prerequisites for this module:** Completed introduction and Satellite configuration (modules 01–05); rhel1.lab terminal accessible
- **Estimated duration:** 5 minutes

## Learning Objectives

- Create a Containerfile that extends a bootc base image with a custom OS-level configuration.
- Build a tagged bootc container image using Podman targeting the Satellite container registry namespace.

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Switch to rhel1.lab terminal and create the Containerfile | 2 min |
| 2 | Build the image with podman build | 3 min |

## Detailed Steps

1. Click the `rhel1.lab terminal` tab in the showroom UI (wetty at /wetty_rhel1).
2. Create the Containerfile by running the following heredoc command:
   ```bash
   cat <<'EOT' > Containerfile
   FROM registry.redhat.io/rhel10/rhel-bootc:10.1
   RUN printf '%s\n' '  _______' ' /       \' '|  o   o  |' '|    ^    |' '|  \___/  |' ' \_______/' > /etc/motd
   EOT
   ```
3. Observe that the Containerfile extends `rhel10/rhel-bootc:10.1` and writes a multi-line ASCII art happy face to `/etc/motd`.
4. Build the image with the following command:
   ```bash
   podman build -f Containerfile -t satellite.lab/acme_org/bootc/rhel-bootc:satellite-image-mode-lab
   ```
5. Wait for the build to complete. The image tag `satellite.lab/acme_org/bootc/rhel-bootc:satellite-image-mode-lab` assigns the image a name that corresponds to its destination in the Satellite container registry.
6. Confirm the build completed successfully by reviewing the final output line from podman.

## Key Takeaways

- Bootc container images are built like any OCI container image — a Containerfile extending the bootc base image with OS-level changes (packages, files, services) constitutes a new OS image version.
- The `/etc/motd` change is a simple but visible customization that will be confirmed after rhel2 reboots into the new image in module-09.
- The image tag path `satellite.lab/acme_org/bootc/rhel-bootc:satellite-image-mode-lab` maps directly to the Satellite registry hostname, organization, product, repository, and tag — this alignment is required for the push in the next module.
- The base image `registry.redhat.io/rhel10/rhel-bootc:10.1` is pre-pulled on rhel1 in this lab environment; in production, participants would need to authenticate to registry.redhat.io first.

## Infrastructure Notes

- Terminal used: rhel1.lab terminal (/wetty_rhel1).
- The rhel10/rhel-bootc:10.1 image is pre-staged on rhel1 by setup automation — no external registry pull occurs during `podman build`.
- The podman build command may take 1–3 minutes depending on available system resources; participants should wait for completion before proceeding.
- The Containerfile uses a heredoc to avoid multi-line paste issues in the wetty terminal.
