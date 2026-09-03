# Module Outline: module-05-verify-host

## Brief Overview

With rhel2 registered, this module explores the image mode information Satellite can collect and display. Participants navigate to the Container Images section in the Satellite Web UI, schedule a "Bootc Status - Script Default" remote job against rhel2 to pull current image mode metadata, and then review the Image Mode Details card on the rhel2 host detail page. The module uses three collapsible steps and is GUI-only.

## Audience and Time

- **Target personas:** Systems administrators, platform engineers
- **Prerequisites for this module:** rhel2 registered to Satellite (module-04 complete)
- **Estimated duration:** 4 minutes

## Learning Objectives

- Explore the Container Images section in Satellite to identify booted image mode hosts.
- Schedule a Bootc Status remote job to collect image mode metadata from a managed host.
- Review image mode details on a host's detail page in Satellite.

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | View booted container images | 1.5 min |
| 2 | Update the container image status (schedule Bootc Status job) | 1.5 min |
| 3 | View image mode details | 1 min |

## Detailed Steps

**Step 1 — View booted container images:**
1. Navigate back to the Satellite Web UI tab.
2. Click "Container images" in the navigation menu.
3. Observe that one image mode host is detected.
4. Click the "Booted" tab.
5. Under the "Hosts" column, click the number `1` link to view the host.

**Step 2 — Update the container image status (schedule Bootc Status remote job):**
1. Check the checkbox for "rhel2.lab" in the host list.
2. Click "Schedule a Job".
3. In the job category dropdown, select "Bootc".
4. Select "Bootc Status - Script Default".
5. Click "Run on selected hosts".
6. On the Jobs menu, click the accordion button next to "rhel2.lab" to expand the job output.
7. Review the output, which shows the image the host was booted from and other bootc metadata.

**Step 3 — View image mode details:**

1. Click on "rhel2.lab" to navigate to the host detail page.
2. Click the "Details" tab.
3. Scroll down to the "Image mode details" card.
4. Note the "Running image" field — this value will be needed context in later modules.

## Key Takeaways

- Satellite 6.19 surfaces image mode host information under "Container images", providing a fleet-wide view of which bootc images are in use.
- The Bootc Status remote job uses Rex (Remote Execution) to collect current image metadata from managed hosts on demand; data is also refreshed approximately every 4 hours automatically.
- The Image Mode Details card on the host detail page shows the currently booted image, staged image (if any), and rollback image.

## Infrastructure Notes

- GUI-only module — no CLI commands.
- The Satellite Web UI Container Images section may show rhel2 only after the Bootc Status job has been run; scheduling this job is the key step that populates the image mode details.
- Remote Execution (Rex) must be configured on the Satellite and reachable on rhel2 — this is handled by the setup automation.
