# Module Outline: module-03-activation-key

## Brief Overview

This module creates the activation key that will be used to register the image mode host rhel2 with Satellite. An activation key in Satellite bundles together a lifecycle environment and content view so that registered hosts automatically receive the right subscriptions and content. Participants create a "bootc" activation key assigned to the Library lifecycle environment with the Default Organization View.

## Audience and Time

- **Target personas:** Systems administrators, platform engineers
- **Prerequisites for this module:** Satellite Web UI session active (module-01 complete); "bootc" product created (module-02 complete)
- **Estimated duration:** 2 minutes

## Learning Objectives

- Create a Satellite activation key that grants a host access to a content view and lifecycle environment.

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Navigate to Activation Keys | 30 sec |
| 2 | Create the "bootc" activation key | 1 min |
| 3 | Assign content view environment | 30 sec |

## Detailed Steps

1. In the Satellite Web UI, navigate to the Activation Keys menu.
2. Click "Create Activation Key".
3. In the Name field, enter `bootc`.
4. Click "Assign content view environments".
5. In the "Assign content view environments" panel, click "Library".
6. Select the "Default Organization View" content view.
7. Click "Save" to confirm the content view environment assignment.
8. Back on the New Activation Key form, click "Save" to create the key.
9. Confirm the "bootc" activation key appears in the Activation Keys list.

## Key Takeaways

- Activation keys streamline host registration by bundling lifecycle environment and content view selection into a single reusable credential.
- The Library lifecycle environment is appropriate for this lab; it provides access to the most recent synced content without promoting through stages.
- This activation key will be referenced by name (`bootc`) in the hammer registration command in module-04.

## Infrastructure Notes

- Navigation path: Content menu (or direct URL) → Activation Keys.
- No CLI commands are used in this module.
- The "Default Organization View" content view is pre-existing in a fresh Satellite installation and does not require prior configuration.
