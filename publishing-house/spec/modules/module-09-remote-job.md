# Module Outline: module-09-remote-job

## Brief Overview

This final module brings together everything from the previous modules. Participants schedule a "Bootc Switch - Script Default" remote job in Satellite targeting rhel2, paste the image label obtained in module-08, and run the job. After the job completes, they switch to the rhel2 terminal to check bootc status (which shows the new image is staged but not yet active), reboot rhel2 into the new image, and confirm the custom MOTD is displayed upon reconnection. A final `bootc status` run confirms rhel2 is running the Satellite-managed image and can roll back to the previous version.

## Audience and Time

- **Target personas:** Systems administrators, platform engineers
- **Prerequisites for this module:** Image label obtained (module-08 complete); rhel2 registered and image mode details verified (modules 04–05 complete)
- **Estimated duration:** 6 minutes

## Learning Objectives

- Schedule a Satellite "Bootc Switch" remote job to stage a new container image on a managed image mode host.
- Verify staged image status using `bootc status` and reboot the host into the new image.
- Confirm the deployed image change by observing the updated MOTD and reviewing `bootc status` output.

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Schedule the Bootc Switch remote job | 2 min |
| 2 | Check bootc status on rhel2 (image staged, not yet active) | 1 min |
| 3 | Reboot rhel2 into the new image | 2 min |
| 4 | Verify updated MOTD and final bootc status | 1 min |

## Detailed Steps

**Step 1 — Schedule the Bootc Switch remote job:**
1. In the Satellite Web UI, go to Hosts > All Hosts.
2. Check the checkbox for "rhel2".
3. Click "Schedule a Job".
4. In the Category and template section, select Job category: "Bootc".
5. Select template: "Bootc Switch - Script Default".
6. Click "Next".
7. In the Target hosts and inputs section, paste the image label into the target field:
   `satellite.lab/acme_org/bootc/rhel-bootc:satellite-image-mode-lab`
8. Click "Run on selected hosts".
9. On the Jobs menu, expand the output for rhel2.lab by clicking the accordion next to "rhel2.lab".
10. Wait for the job to complete successfully.

**Step 2 — Check bootc status before reboot:**
1. Click the `rhel2.lab terminal` tab (wetty at /wetty_rhel2).
2. Run: `bootc status`
3. Observe the output showing the new image (`satellite.lab/acme_org/bootc/rhel-bootc:satellite-image-mode-lab`) is staged but rhel2 is still booted from the old image (`registry.redhat.io/rhel10/rhel-bootc:10.1`).

**Step 3 — Reboot into the new image:**
1. In the rhel2.lab terminal, run: `reboot`
2. Wait for rhel2 to reboot. The wetty terminal will lose connection.
3. If the terminal appears stuck, click the refresh button to reconnect.
4. Reconnect when the terminal becomes available.

**Step 4 — Verify the update:**
1. Observe the terminal login prompt displaying the new custom ASCII happy face MOTD.
2. Run: `bootc status`
3. Confirm the output shows rhel2 is now running `satellite.lab/acme_org/bootc/rhel-bootc:satellite-image-mode-lab`.
4. Note that the previous image (`registry.redhat.io/rhel10/rhel-bootc:10.1`) is listed as the rollback image.

## Key Takeaways

- The Bootc Switch remote job uses Satellite Remote Execution (Rex) to instruct the image mode host to stage the new container image; the image is not applied until the host reboots.
- `bootc status` before the reboot shows the staged image vs. the running image — this dual-state view is a key safety feature of image mode.
- After rebooting, the previously running image is retained as a rollback target — participants can roll back to the previous OS image without re-deploying from scratch.
- The custom MOTD from the Containerfile modification in module-06 is now visible on every login, confirming the image update was applied end-to-end through the full bootc lifecycle: Containerfile → Podman build → Satellite registry → remote job → reboot.

## Infrastructure Notes

- Terminals used: Satellite Web UI (for the remote job), rhel2.lab terminal (/wetty_rhel2, for bootc status and reboot).
- The reboot typically takes 1–2 minutes. The wetty terminal will disconnect and reconnect automatically or after a manual refresh.
- The rollback image entry in `bootc status` after the reboot confirms the bootloader has two boot entries; participants do not need to perform a rollback, but should note the capability.
- The Bootc Switch job uses the image label as a pull reference; rhel2 must be able to reach satellite.lab on the container registry port (typically 443) to pull the new image layers during staging.
