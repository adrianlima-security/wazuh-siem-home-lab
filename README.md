# Wazuh SIEM Home Lab

![Platform](https://img.shields.io/badge/Platform-Wazuh-blue)
![OS](https://img.shields.io/badge/OS-Ubuntu%2024.04%20%7C%20Windows%2011-green)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)
![License](https://img.shields.io/badge/Project-Home%20Lab-red)

---

# Overview

This project documents the implementation of a Wazuh SIEM Home Lab designed to simulate a Security Operations Center (SOC) monitoring and detection environment.

The objective is to gain hands-on experience with SIEM deployment, endpoint monitoring, Windows Event Log collection, PowerShell monitoring, security alert investigation, attack simulation, MITRE ATT&CK mapping, and SOC analyst workflows.

The laboratory reproduces a defensive security environment where endpoint telemetry is collected, analyzed, and investigated through a centralized SIEM platform.

---

# Objectives

* Deploy a functional Wazuh SIEM environment.
* Configure endpoint monitoring.
* Collect Windows security telemetry.
* Analyze authentication and privilege-related activity.
* Monitor PowerShell execution.
* Investigate security alerts.
* Simulate attacker techniques.
* Map detected activity to MITRE ATT&CK.
* Practice SOC investigation workflows.
* Develop practical blue team and detection engineering skills.

---

# Lab Architecture

```text
              Windows 11 Endpoint
                     │
                     │
               Wazuh Agent
                     │
                     │
               Wazuh Manager
                     │
                     │
        Wazuh Indexer + Dashboard
                     │
                     │
        Security Alert Investigation
                     │
                     │
        MITRE ATT&CK Technique Mapping
```

---

# Environment

## SIEM Platform

* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard

## Server

* Ubuntu Server 24.04 LTS

## Endpoint

* Windows 11
* Wazuh Agent

---

# Technologies Used

## Security

* Wazuh SIEM/XDR
* Windows Event Logs
* PowerShell Script Block Logging
* Security Monitoring
* Endpoint Detection and Response (EDR) Concepts
* MITRE ATT&CK Framework

## Infrastructure

* Ubuntu Server
* Windows 11 Virtual Machine
* VMware Workstation
* Git
* GitHub

---

# Project Phases

## Phase 1 – Environment Preparation

Implemented:

* Laboratory planning
* Virtual machine preparation
* Network configuration
* Initial environment validation

---

## Phase 2 – Wazuh Deployment

Implemented:

* Wazuh Manager installation
* Wazuh Indexer installation
* Wazuh Dashboard deployment
* SIEM platform validation

---

## Phase 3 – Agent Deployment

Implemented:

* Windows 11 endpoint deployment
* Wazuh Agent installation
* Agent registration
* Communication validation

---

## Phase 4 – Log Collection

Implemented:

* Windows Event collection
* Security log ingestion
* Endpoint telemetry validation

---

## Phase 5 – Security Monitoring

Implemented:

* Dashboard investigation
* Event filtering
* Security event analysis
* Endpoint activity monitoring

---

## Phase 6 – Detection Validation

Implemented:

* Authentication monitoring
* Privileged account activity analysis
* Security event validation

Analyzed events:

* Event ID 4624 — Successful Logon
* Event ID 4672 — Special Privileges Assigned

---

## Phase 7 – Windows Event Monitoring & PowerShell Detection

Implemented:

* Windows Security Event monitoring
* Authentication event analysis
* Privilege monitoring
* Credential Manager visibility
* PowerShell Script Block Logging
* PowerShell command detection

Detected Windows Events:

* Event ID 4624 — Successful Logon
* Event ID 4672 — Special Privileges Assigned
* Event ID 5379 — Credential Manager Access
* Event ID 4104 — PowerShell Script Block Logging

PowerShell activity successfully captured:

* `whoami`
* `hostname`
* `Get-Date`
* `Get-WinEvent`

---

## Phase 8 – MITRE ATT&CK Simulation & Detection Validation

Implemented:

* Controlled attack simulation
* PowerShell-based reconnaissance activity
* Security alert investigation
* MITRE ATT&CK technique mapping

Attack simulation:

```powershell
Get-Process
```

The activity simulated attacker behavior attempting to enumerate running processes on a Windows endpoint.

Detection:

* PowerShell Script Block Logging
* Windows Event ID 4104
* Wazuh alert generation

MITRE ATT&CK Mapping:

```
T1057 - Process Discovery
```

The exercise validated the complete detection workflow:

```
Attack Simulation
        ↓
Telemetry Generation
        ↓
Log Collection
        ↓
SIEM Detection
        ↓
Alert Investigation
        ↓
MITRE ATT&CK Classification
```

---

# Key Findings

The SIEM successfully collected, processed, and displayed Windows endpoint telemetry.

PowerShell Script Block Logging provided visibility into executed PowerShell commands, allowing Wazuh to analyze endpoint activity and generate security alerts.

The laboratory successfully demonstrated:

* Endpoint telemetry collection.
* Windows event analysis.
* PowerShell monitoring.
* Security alert investigation.
* Attack simulation and detection validation.
* MITRE ATT&CK classification.

---

# Repository Structure

```
wazuh-siem-home-lab/
│
├── documentation/
│   │
│   ├── phase-1-environment-setup.md
│   ├── phase-2-wazuh-deployment.md
│   ├── phase-3-agent-deployment.md
│   ├── phase-4-log-collection.md
│   ├── phase-5-security-monitoring.md
│   ├── phase-6-detection-validation.md
│   ├── phase-7-windows-event-monitoring.md
│   └── phase-8-mitre-attack-detection.md
│
├── screenshots/
│
└── README.md
```

---

# Documentation

Detailed documentation is available in the **documentation/** directory.

Current documentation:

* Phase 7 – Windows Event Monitoring and PowerShell Detection
* Phase 8 – MITRE ATT&CK Simulation and Detection Validation

---

# Screenshots

Implementation evidence is stored in the **screenshots/** directory.

Current screenshots include:

* Wazuh Dashboard monitoring
* Windows authentication events
* Failed logon detection
* Privilege escalation related events
* PowerShell Event ID 4104
* Script Block Logging
* MITRE ATT&CK detection alert
* Security alert investigation

---

# Skills Demonstrated

## SIEM Operations

* Wazuh administration
* Event ingestion
* Log analysis
* Alert investigation

## Security Monitoring

* Windows Event Log analysis
* Authentication monitoring
* Privilege monitoring
* Endpoint visibility

## Threat Detection

* PowerShell activity analysis
* Script Block Logging
* Attack simulation
* MITRE ATT&CK mapping
* Detection validation

## Cybersecurity Concepts

* SIEM architecture
* Endpoint monitoring
* Detection engineering
* Defensive security
* SOC analyst workflows
* Blue team operations

---

# Future Improvements

Planned enhancements include:

* Linux endpoint monitoring
* Sysmon integration
* Custom Wazuh detection rules
* Atomic Red Team simulations
* Threat Intelligence integration
* Active Response automation
* Sigma rule integration
* Additional MITRE ATT&CK scenarios

---

# Conclusion

This project demonstrates the implementation of a functional Wazuh SIEM environment focused on security monitoring, detection validation, and SOC investigation workflows.

The laboratory provides practical experience in deploying a SIEM, monitoring Windows endpoints, collecting security telemetry, investigating alerts, simulating attacker behavior, and mapping detected activity to the MITRE ATT&CK framework.

The project reflects practical SOC analyst activities, including event monitoring, PowerShell analysis, authentication investigation, threat detection, and defensive security operations.

**This repository is actively being expanded with additional detection scenarios, attack simulations, and SOC use cases.**