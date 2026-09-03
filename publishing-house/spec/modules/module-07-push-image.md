# Module Outline: module-07-push-image

## Brief Overview

With the custom bootc image built on rhel1, this module pushes it to the Satellite embedded container registry. Participants first authenticate Podman to the Satellite registry using the Satellite admin credentials, then push the tagged image. After this module, the image is stored in the "bootc" product on Satellite and available to be deployed to managed hosts.

## Audience and Time

- **Target personas:** Systems administrators, platform engineers
- **Prerequisites for this module:** Image built and tagged on rhel1 (module-06 complete); Satellite "bootc" product created (module-02 complete)
- **Estimated duration:** 3 minutes

## Learning Objectives

- Authenticate Podman to the Satellite embedded container registry and push a bootc image.

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Log into the Satellite container registry | 1 min |
| 2 | Push the image | 2 min |

## Detailed Steps

1. Remain in the `rhel1.lab terminal` (wetty at /wetty_rhel1).
2. Log into the Satellite container registry with:
   ```bash
   podman login --tls-verify=false satellite.lab --username admin --password bc31c9a6-9ff0-11ec-9587-00155d1b0702
   ```
3. Confirm the login succeeds ("Login Succeeded" message).
4. Push the image to Satellite with:
   ```bash
   podman push satellite.lab/acme_org/bootc/rhel-bootc:satellite-image-mode-lab --tls-verify=false
   ```
5. Wait for the push to complete. Layers will upload progressively; the final line confirms the push.

## Key Takeaways

- The Satellite embedded container registry accepts standard OCI image pushes via Podman (or any OCI-compliant tool) authenticated with Satellite credentials.
- The `--tls-verify=false` flag bypasses TLS certificate verification for the self-signed Satellite certificate in this lab environment; in production, the certificate would be trusted.
- The image path in the registry mirrors the product/repository structure in Satellite: `satellite.lab` (host) / `acme_org` (organization) / `bootc` (product) / `rhel-bootc` (repository) : `satellite-image-mode-lab` (tag).

## Infrastructure Notes

- Terminal used: rhel1.lab terminal (/wetty_rhel1).
- The push transfers image layers from rhel1 to satellite.lab over the internal lab network — no external internet egress is needed.
- `--tls-verify=false` is required because the Satellite TLS certificate is self-signed and not trusted by the system CA bundle on rhel1.
- The push may take 1–2 minutes depending on image size and lab network throughput.
