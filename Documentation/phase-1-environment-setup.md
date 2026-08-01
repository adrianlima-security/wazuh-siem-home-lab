# Phase 1 - Environment Setup

## Objective

The objective of this phase is to prepare the virtual environment required for the deployment of a Wazuh SIEM laboratory.

The goal is to create a controlled cybersecurity lab environment where security events can be collected, monitored and analyzed.

---

## Lab Architecture

The initial laboratory environment will consist of:

- Host machine: Windows 11
- Hypervisor: VMware Workstation
- Server operating system: Ubuntu Server 24.04 LTS
- SIEM Platform: Wazuh

---

## Environment Preparation

The following components will be installed and configured:

### Virtualization Platform

Software:
- VMware Workstation

Purpose:
- Create and manage virtual machines required for the security laboratory.


### Ubuntu Server

Operating System:
- Ubuntu Server 24.04 LTS

Purpose:
- Host the Wazuh Manager components.


---

## Virtual Machine Configuration

Planned configuration:

Machine name:

Wazuh-Server


Resources:

CPU:
4 cores


RAM:
8 GB


Storage:
80 GB


Network:
NAT


---

## Implementation Status

Current status:

In progress


Completed tasks:

- Created GitHub repository
- Created project structure
- Created documentation framework


Pending tasks:

- Install VMware Workstation
- Deploy Ubuntu Server virtual machine
- Configure server environment


---

## Next Phase

Phase 2 will cover the installation and initial configuration of Wazuh SIEM.