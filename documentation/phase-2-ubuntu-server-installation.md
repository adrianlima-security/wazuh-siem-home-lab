# Phase 2 - Ubuntu Server Installation

## Objective

The objective of this phase is to install Ubuntu Server 24.04 LTS and perform the initial operating system configuration required for the Wazuh SIEM/XDR deployment.

---

## Installation Summary

The Ubuntu Server operating system was successfully installed on the previously created virtual machine.

The installation was completed using the default Ubuntu Server installer.

---

## System Information

| Item | Configuration |
|------|---------------|
| Operating System | Ubuntu Server 24.04.4 LTS |
| Hostname | wazuh-server |
| Username | adrian |
| Hypervisor | VMware Workstation Pro |
| Network Mode | NAT |

---

## Installation Steps Completed

- Booted the virtual machine.
- Started the Ubuntu Server installer.
- Selected English language.
- Configured English (US) keyboard layout.
- Used automatic network configuration (DHCP).
- Configured NAT networking.
- Used the default Ubuntu package mirror.
- Configured automatic disk partitioning.
- Created the administrator user.
- Installed OpenSSH Server.
- Completed the operating system installation.
- Rebooted the virtual machine.
- Successfully logged into Ubuntu Server.

---

## Current System Status

The server booted successfully after installation.

The network interface received an IP address automatically through DHCP.

The operating system is ready for the initial configuration.

---

## Evidence

Screenshots collected during this phase:

- VM boot process.
- Ubuntu Server installer.
- Network configuration.
- Storage configuration.
- First successful login.

All screenshots are stored in the `screenshots` directory.

---

## Next Phase

The next phase will cover:

- Updating the operating system.
- Installing required packages.
- Verifying network connectivity.
- Preparing the server for the Wazuh installation.