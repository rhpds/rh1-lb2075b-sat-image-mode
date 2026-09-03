# Module Outline: module-01-introduction

## Brief Overview

This opening module sets the stage for the entire lab. It introduces RHEL image mode (bootc) — a container-native approach to deploying and managing the operating system — and explains how Red Hat Satellite 6.19 provides management capabilities for bootc hosts. The module describes the three-node lab environment (one Satellite server and two RHEL 10 hosts) and walks participants through logging into the Satellite Web UI for the first time. No prior Satellite experience is assumed.

## Audience and Time

- **Target personas:** Systems administrators, platform engineers
- **Prerequisites for this module:** None — this is the entry point
- **Estimated duration:** 3 minutes

## Learning Objectives

- Identify the role of RHEL image mode (bootc) in container-native OS lifecycle management.
- Navigate to the Satellite Web UI and authenticate using the provided credentials.

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Image Mode — bootc concept and eight-module summary | 1 min |
| 2 | Lab Environment — environment diagram review | 1 min |
| 3 | Log into the Web UI | 1 min |

## Detailed Steps

1. Read the introductory text explaining RHEL image mode (bootc) and how Satellite 6.19 manages bootc systems.
2. Review the summary of the eight upcoming modules listed in the introduction.
3. Note the lab environment components: satellite.lab (Satellite server), rhel1.lab (RHEL 10 builder node), rhel2.lab (RHEL 10 image mode host).
4. Click on the "Satellite Web UI" tab in the showroom interface.
5. Enter the username `admin` in the login form.
6. Enter the provided password `bc31c9a6-9ff0-11ec-9587-00155d1b0702` in the password field.
7. Click "Log In".
8. Confirm you are taken to the Satellite main dashboard.

## Key Takeaways

- RHEL image mode (bootc) treats the OS as a container image, enabling container-native build, deploy, and update workflows.
- Red Hat Satellite 6.19 adds management capabilities for image mode hosts, including registration, status reporting, and remote job execution.
- The lab environment consists of one Satellite server and two RHEL 10 hosts — one builder and one image mode managed host.

## Infrastructure Notes

- Satellite 6.19 is pre-installed on satellite.lab; installation is out of scope for this lab.
- The Satellite Web UI tab must be reachable from the showroom UI at lab start.
- Admin credentials are hardcoded in the lab content: username `admin`, password `bc31c9a6-9ff0-11ec-9587-00155d1b0702`.
