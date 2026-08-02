# Phase 3 - Initial Server Configuration

## Objective

The objective of this phase is to perform the initial configuration and validation of the Ubuntu Server environment before deploying the Wazuh SIEM/XDR platform.

This phase includes connectivity verification, system updates, hostname validation, network configuration checks, time synchronization verification, SSH service configuration and system resource validation.

---

## Step 1 - Network Connectivity Verification

### Description

Before installing additional software, the server connectivity was verified to ensure that the system had access to external resources.

Command executed:

```bash
ping -c 4 google.com
```

### Result

The server successfully reached external hosts.

The connectivity test confirmed:

- Internet access available.
- Packets transmitted successfully.
- No packet loss detected.

### Evidence

Screenshot:

`phase3-01-network-connectivity.png`

---

## Step 2 - Package Repository Update

### Description

The package repository information was updated to ensure that the server had access to the latest available software versions.

Command executed:

```bash
sudo apt update
```

### Result

The package lists were successfully updated.

### Evidence

Screenshot:

`phase3-02-apt-update.png`

---

## Step 3 - System Upgrade

### Description

The operating system packages were upgraded to ensure the server was running the latest available updates before the Wazuh deployment.

Command executed:

```bash
sudo apt upgrade -y
```

### Result

The system upgrade completed successfully.

### Evidence

Screenshot:

`phase3-03-system-upgrade.png`

---

## Step 4 - Hostname Verification

### Description

The hostname configuration was verified to confirm that the server identity matched the planned Wazuh deployment environment.

Command executed:

```bash
hostnamectl
```

### Result

The hostname was confirmed as:

```text
wazuh-server
```

### Evidence

Screenshot:

`phase3-04-hostname-verification.png`

---

## Step 5 - Network Configuration Verification

### Description

The network interface configuration was reviewed to confirm that the server received an IP address through the VMware NAT configuration.

Command executed:

```bash
ip a
```

### Result

The server successfully obtained an IP address through DHCP.

### Evidence

Screenshot:

`phase3-05-ip-address.png`

---

## Step 6 - Time Synchronization Verification

### Description

Time synchronization was checked because accurate timestamps are essential for security monitoring, log correlation and incident investigation.

Command executed:

```bash
timedatectl
```

### Result

The system time synchronization service was verified successfully.

### Evidence

Screenshot:

`phase3-06-time-synchronization.png`

---

## Step 7 - SSH Service Configuration

### Description

The SSH service was verified to ensure remote administration capability.

During the verification process, the SSH service was found installed but inactive.

The service was started and configured to automatically start after system reboot.

Commands executed:

```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```

Verification commands:

```bash
systemctl status ssh
systemctl is-enabled ssh
```

### Result

The SSH service was successfully configured.

Service status:

```text
Active: active (running)
```

Startup configuration:

```text
enabled
```

This ensures that remote administration remains available after server restarts.

### Evidence

Screenshots:

`phase3-07-ssh-running.png`

`phase3-08-ssh-enabled.png`

---

## Step 8 - System Resource Verification

### Description

The server resources were reviewed before the Wazuh installation to confirm that the virtual machine had sufficient capacity.

Commands executed:

### Memory

```bash
free -h
```

### CPU

```bash
lscpu
```

### Storage

```bash
df -h
```

### Result

The system resources were verified and the server is ready for the Wazuh deployment phase.

### Evidence

Screenshots:

`phase3-09-memory.png`

`phase3-10-cpu.png`

`phase3-11-disk-space.png`

---

## Environment Validation

The server has been successfully validated and meets the requirements for the Wazuh deployment.

Validated components:

- Internet connectivity.
- Updated Ubuntu packages.
- Correct hostname configuration.
- Network availability.
- System time synchronization.
- SSH remote administration.
- Available system resources.

---

# Phase 3 Summary

The Ubuntu Server environment has been successfully prepared for the Wazuh SIEM/XDR deployment.

Completed tasks:

- Network connectivity verified.
- Operating system updated.
- Hostname validated.
- Network configuration checked.
- Time synchronization verified.
- SSH service configured.
- System resources validated.

The server is now ready for the Wazuh installation phase.

---

# Next Phase

The next phase will cover:

- Wazuh Manager installation.
- Wazuh Indexer deployment.
- Wazuh Dashboard installation.
- Initial platform verification.