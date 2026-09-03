# Module Outline: module-02-container-repository

## Brief Overview

In this module, participants create the Satellite content structure needed to store image mode container images. They create a "bootc" Product in Satellite — a logical grouping that contains a container repository — which will later hold the custom bootc image built on rhel1. This is a short, GUI-only module consisting of three clicks and a form submission.

## Audience and Time

- **Target personas:** Systems administrators, platform engineers
- **Prerequisites for this module:** Logged into the Satellite Web UI (completed in module-01)
- **Estimated duration:** 2 minutes

## Learning Objectives

- Create a Satellite Product to serve as a container repository for image mode images.

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Navigate to Content > Products | 30 sec |
| 2 | Create the "bootc" product | 1 min |
| 3 | Confirm product creation | 30 sec |

## Detailed Steps

1. In the Satellite Web UI, expand the "Content" menu in the left navigation bar.
2. Click "Products".
3. Click "Create Product".
4. In the Name field, enter `bootc`.
5. Click "Save".
6. Confirm the "bootc" product appears in the Products list.

## Key Takeaways

- Satellite Products are logical containers that group repositories; a container repository under a Product is where pushed images will be stored.
- The "bootc" product name is referenced throughout later modules — the product name must match exactly when pushing and retrieving images.

## Infrastructure Notes

- The Satellite Web UI is accessed from the "Satellite Web UI" showroom tab.
- No CLI commands are used in this module.
- The product creation does not require any subscription or content view configuration at this stage.
