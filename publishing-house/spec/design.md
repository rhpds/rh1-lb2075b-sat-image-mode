# Satellite Image Mode: Registering and Updating RHEL Image Mode Hosts with Red Hat Satellite 6.19

## Overview

This lab introduces RHEL image mode (bootc), a container-native approach to operating system lifecycle management, and demonstrates how Red Hat Satellite 6.19 manages bootc systems at scale. Participants register a pre-built image mode host to a Satellite server, create the required container product and activation key, build a customized bootc container image on a builder node, push it to Satellite's embedded container registry, and use Satellite remote jobs to stage and apply the update on the managed host. The entire workflow — from registration through update and verification — is completed in approximately 30 minutes.

## Target Audience

- **Role:** Systems administrators, platform engineers
- **Experience level:** Intermediate
- **What they already know:** Basic Linux CLI usage, basic container image concepts (what an image is, what a tag is, what a registry is), familiarity with web-based administration UIs
- **What they don't know:** How to register RHEL image mode (bootc) hosts to Red Hat Satellite, how Satellite manages container-based OS images, how to use Satellite remote jobs to update bootc systems

## Prerequisites

- Basic familiarity with Linux command-line operations
- Basic understanding of container image concepts (image, tag, registry)
- No prior Red Hat Satellite experience required; all Satellite configuration is performed from scratch during the lab
- The lab can partially validate prerequisites automatically: SSH access from satellite.lab to rhel2.lab is confirmed by the registration step, and Satellite pre-installation is verified by the Web UI being accessible at lab start

## Learning Objectives

1. Register a RHEL image mode host to Red Hat Satellite 6.19 by creating a container product, activation key, and executing a hammer-generated registration command via SSH.
2. Build, push, and deploy a customized bootc container image to a managed host using Satellite's embedded container registry and Satellite remote jobs.

## Content Type

Lab (hands-on)

## Products & Technologies

- Red Hat Satellite 6.19
- Red Hat Enterprise Linux 10
- RHEL Image Mode (bootc)
- Podman
- hammer CLI
- Red Hat Container Registry (registry.redhat.io) — base image pre-staged in lab environment
- Satellite embedded container registry
- Satellite Remote Jobs (Rex)

## Module Map

| Module | Title | Duration |
|--------|-------|----------|
| 1 | Image Mode Introduction | 3 min |
| 2 | Create Container Repository | 2 min |
| 3 | Create Activation Key | 2 min |
| 4 | Register Image Mode Host | 3 min |
| 5 | Verify Image Mode Host Details | 4 min |
| 6 | Update Container Image | 5 min |
| 7 | Push Container Image | 3 min |
| 8 | Obtain Image Label | 2 min |
| 9 | Schedule Remote Job | 6 min |
| — | **Total hands-on** | **30 min** |
| — | Intro / presentation | ~0 min |
| — | **Total lab** | **~30 min** |

## Difficulty Level

Intermediate

## Environment

**Learner view:** The lab starts with three pre-provisioned hosts: satellite.lab (Satellite 6.19 installed and running, Web UI accessible, embedded container registry active), rhel1.lab (RHEL 10 builder node with Podman installed and the rhel10/rhel-bootc:10.1 base image pre-pulled), and rhel2.lab (RHEL 10 pre-built as a bootc system, SSH-accessible from satellite.lab as root). Participants interact via three wetty terminal tabs (/wetty_satellite, /wetty_rhel1, /wetty_rhel2) and the Satellite Web UI tab. No Satellite content configuration is pre-done — participants create all products, activation keys, and remote job runs from scratch during the lab.

**Automation needed:** Yes

Pre-provisioned resources: Satellite 6.19 installed and running on satellite.lab with the Satellite admin credentials pre-set; rhel10/rhel-bootc:10.1 image pre-pulled on rhel1.lab; rhel2.lab booted as a bootc system and reachable via SSH from satellite.lab; wetty terminal sessions available on all three hosts; Satellite Web UI accessible from the lab tab.

## Infrastructure Requirements

- **Cloud provider:** TBD — confirmed in infrastructure phase
- **Cluster type:** TBD — confirmed in infrastructure phase
- **OCP version:** TBD — confirmed in infrastructure phase
- **Topology:** TBD — confirmed in infrastructure phase
- **Sizing:** TBD — confirmed in infrastructure phase
- **Automation approach:** TBD — confirmed in infrastructure phase
- **AI/MaaS:** TBD — confirmed in infrastructure phase
- **External services:** TBD — confirmed in infrastructure phase
- **AAP version:** TBD — confirmed in infrastructure phase
- **Non-GA products:** TBD — confirmed in infrastructure phase

## Assessment Strategy (Optional)

This is a Zero-Touch lab. Each module has solve and validation scripts attached to the runtime automation. The solve script executes all participant commands for that module; the validation script checks that the expected system state is achieved before allowing progression. For GUI-only modules (create container product, create activation key, obtain image label), validation confirms the resulting Satellite API state — product exists, activation key exists, image tag is accessible in the registry. For CLI modules, validation checks command output and system state: host registered in Satellite after module 4, image successfully built and tagged after module 6, image present in Satellite registry after module 7, and bootc status showing the correct running image after module 9.
