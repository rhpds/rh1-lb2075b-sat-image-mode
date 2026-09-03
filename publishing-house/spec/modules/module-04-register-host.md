# Module Outline: module-04-register-host

## Brief Overview

This module registers the pre-built image mode host rhel2 with Satellite. Participants use the hammer CLI on satellite.lab to generate a host registration command that references the "bootc" activation key created in the previous module, then pipe that command via SSH into rhel2. The result is a registered image mode host visible in Satellite's host inventory.

## Audience and Time

- **Target personas:** Systems administrators, platform engineers
- **Prerequisites for this module:** "bootc" activation key created (module-03 complete); rhel2.lab reachable via SSH from satellite.lab as root
- **Estimated duration:** 3 minutes

## Learning Objectives

- Generate a Satellite host registration command using the hammer CLI and apply it to a remote image mode host via SSH.

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Switch to satellite.lab terminal | 30 sec |
| 2 | Run the hammer + SSH registration command | 2 min |
| 3 | Confirm successful registration in output | 30 sec |

## Detailed Steps

1. Click the `satellite.lab terminal` tab in the showroom UI (wetty at /wetty_satellite).
2. Run the following compound command (using the showroom run button or copy-paste):
   ```bash
   export regscript=$(hammer host-registration generate-command --activation-key bootc --setup-insights 0 --insecure 1 --setup-container-registry-certs true --force 1)
   ssh -o "StrictHostKeyChecking no" root@rhel2 $regscript
   ```
3. Wait for the command to complete. Observe the registration output indicating success.
4. Optionally, navigate to Hosts > All Hosts in the Satellite Web UI to confirm rhel2.lab appears in the list.

## Key Takeaways

- `hammer host-registration generate-command` produces a self-contained registration script that can be piped to any target host — useful for automation.
- The `--setup-container-registry-certs true` flag configures the image mode host to trust the Satellite embedded container registry, which is needed for the later image push and switch operations.
- The `--force 1` flag re-registers the host even if it was previously registered; this is safe in a lab environment.
- SSH key trust (`StrictHostKeyChecking no`) is pre-configured in the lab environment between satellite.lab and rhel2.lab.

## Infrastructure Notes

- Terminal used: satellite.lab terminal (/wetty_satellite).
- rhel2.lab must be SSH-accessible as root from satellite.lab without a password prompt (key pre-distributed in lab setup automation).
- The registration command is generated at runtime from Satellite's API, so it is specific to the current lab instance — participants should not hard-code it.
- `--insecure 1` is used because the lab Satellite certificate is self-signed; in production, this flag would not be used.
