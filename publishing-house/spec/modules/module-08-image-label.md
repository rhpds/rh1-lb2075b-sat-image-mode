# Module Outline: module-08-image-label

## Brief Overview

Before scheduling the Bootc Switch remote job, participants need the exact image label (the "Published At" URL) that Satellite assigned to the newly pushed image tag. This module navigates the Satellite Web UI through Content > Products > bootc > Container Image Tags to locate the tag's lifecycle environment entry and copy the published URL. The value is used as input to the remote job in the next module.

## Audience and Time

- **Target personas:** Systems administrators, platform engineers
- **Prerequisites for this module:** Image pushed to Satellite container registry (module-07 complete)
- **Estimated duration:** 2 minutes

## Learning Objectives

- Navigate the Satellite Web UI to locate the published image label for a container image tag.

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Navigate to the bootc product and container image tags | 1 min |
| 2 | Locate and copy the Published At value | 1 min |

## Detailed Steps

1. Return to the Satellite Web UI tab.
2. In the left navigation, go to "Content" > "Products".
3. Click on the "bootc" product.
4. Click "Container Image Tags".
5. Click on the tag `satellite-image-mode-lab`.
6. Click the "Lifecycle Environments" tab.
7. Locate the "Published At" field.
8. Note or copy the value: `satellite.lab/acme_org/bootc/rhel-bootc:satellite-image-mode-lab` — this is the image label that will be pasted into the Bootc Switch job in module-09.

## Key Takeaways

- Satellite tracks each container image tag's publish status across lifecycle environments; the "Published At" URL is the fully qualified image reference that a bootc host can pull from.
- The Published At label combines the Satellite registry hostname, organization, product, repository, and tag into a single pullable URI — it is this value that the Bootc Switch remote job requires to tell the target host which image to stage.

## Infrastructure Notes

- GUI-only module — no CLI commands.
- The Published At value is deterministic in this lab: `satellite.lab/acme_org/bootc/rhel-bootc:satellite-image-mode-lab`. It is shown in the content for participant reference if they cannot navigate to it.
- Navigation path: Content > Products > bootc > Container Image Tags > satellite-image-mode-lab > Lifecycle Environments tab.
