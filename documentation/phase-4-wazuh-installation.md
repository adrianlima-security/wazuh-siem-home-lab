# Phase 4 - Wazuh SIEM/XDR Installation

## Objective

The objective of this phase is to deploy the Wazuh SIEM/XDR platform on the Ubuntu Server environment.

This phase includes downloading the Wazuh installation assistant, validating the installer, troubleshooting the initial download issue, deploying the Wazuh components and verifying the successful installation.

---

## Wazuh Deployment Overview

Wazuh is an open-source SIEM/XDR platform used for security monitoring, log analysis, threat detection and endpoint protection.

The deployment includes the following components:

- Wazuh Indexer
- Wazuh Manager
- Wazuh Dashboard

---

# Step 1 - Download Wazuh Installation Assistant

## Description

The official Wazuh installation assistant was downloaded to automate the deployment of the SIEM/XDR platform.

Command executed:

```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
```

## Verification

The downloaded file was verified:

```bash
ls -l wazuh-install.sh
```

The installer file was successfully downloaded.

## Evidence

Screenshot:

`phase4-01-wazuh-installer-download.png`

---

# Step 2 - Installer Validation

## Description

Before executing the installation script, the file content was reviewed to verify that the downloaded file was a valid Bash script.

Command executed:

```bash
head wazuh-install.sh
```

## Result

The file was confirmed to be a Wazuh installation script.

The script header was verified:

```bash
#!/bin/bash
```

## Evidence

Screenshot:

`phase4-02-wazuh-script-validation.png`

---

# Step 3 - Troubleshooting Initial Download Issue

## Description

During the initial download attempt, the downloaded file did not contain the expected installation script.

The file content showed an XML error response:

```xml
AccessDenied
```

The issue was identified because the downloaded file was not a Bash script.

## Resolution

The incorrect file was removed and the installer was downloaded again using the correct Wazuh package source.

Commands executed:

```bash
rm wazuh-install.sh
```

The installer was downloaded again and successfully validated before execution.

## Result

The correct Wazuh installation assistant was obtained.

---

# Step 4 - Wazuh Installation

## Description

The Wazuh installation assistant was executed to deploy the complete SIEM/XDR environment.

Command executed:

```bash
sudo bash wazuh-install.sh -a
```

The installation process deployed:

- Wazuh Indexer
- Wazuh Manager
- Wazuh Dashboard

## Result

The installation completed successfully.

The Wazuh platform was deployed on the Ubuntu Server environment.

## Evidence

Screenshot:

`phase4-03-wazuh-installation-complete.png`

---

# Step 5 - Installation Validation

## Description

After the installation process, the Wazuh services were verified to confirm that all components were running correctly.

Services validated:

```bash
systemctl status wazuh-manager
```

```bash
systemctl status wazuh-indexer
```

```bash
systemctl status wazuh-dashboard
```

## Result

The Wazuh services were successfully installed and running.

The platform is ready for initial access and configuration.

---

# Phase 4 Summary

The Wazuh SIEM/XDR platform was successfully deployed on the Ubuntu Server environment.

Completed tasks:

- Downloaded Wazuh installation assistant.
- Validated the installation script.
- Identified and resolved an AccessDenied download issue.
- Installed Wazuh Indexer.
- Installed Wazuh Manager.
- Installed Wazuh Dashboard.
- Verified successful deployment.

The server is now ready for the next phase: endpoint deployment and security monitoring.

---

# Next Phase

The next phase will cover:

- Connecting endpoints to Wazuh.
- Deploying Wazuh agents.
- Collecting security events.
- Generating and analyzing alerts.