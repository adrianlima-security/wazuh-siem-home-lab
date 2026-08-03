# Wazuh SIEM Home Lab

![Platform](https://img.shields.io/badge/Platform-Wazuh-blue)
![OS](https://img.shields.io/badge/OS-Ubuntu%2024.04%20%7C%20Windows%2011-green)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)
![License](https://img.shields.io/badge/Project-Home%20Lab-red)

---

# Overview

This project documents the implementation of a Wazuh SIEM Home Lab designed to simulate a Security Operations Center (SOC) monitoring, detection, and investigation environment.

The objective is to gain hands-on experience with SIEM deployment, endpoint monitoring, Windows Event Log collection, PowerShell monitoring, Sysmon integration, security alert investigation, attack simulation, MITRE ATT&CK mapping, and detection engineering workflows.

The laboratory reproduces a defensive security environment where endpoint telemetry is collected, analyzed, investigated, and transformed into actionable security intelligence through a centralized SIEM platform.

---

# Objectives

* Deploy a functional Wazuh SIEM environment.
* Configure endpoint monitoring.
* Collect Windows security telemetry.
* Integrate Sysmon endpoint visibility.
* Analyze authentication and privilege-related activity.
* Monitor PowerShell execution.
* Investigate security alerts.
* Simulate attacker techniques.
* Map detected activity to MITRE ATT&CK.
* Develop and validate detection logic.
* Practice SOC analyst workflows.
* Develop practical blue team and detection engineering skills.

---

# Lab Architecture

```text
              Windows 11 Endpoint
                     │
                     │
        Sysmon + Wazuh Agent
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
                     │
                     │
          Detection Engineering
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
* Microsoft Sysmon

---

# Technologies Used

## Security

* Wazuh SIEM/XDR
* Microsoft Sysmon
* Windows Event Logs
* PowerShell Script Block Logging
* Security Monitoring
* Endpoint Detection and Response (EDR) Concepts
* MITRE ATT&CK Framework
* Detection Engineering

## Infrastructure

* Ubuntu Server
* Windows 11 Endpoint
* VMware Workstation
* Git
* GitHub

---

# Project Phases

## Phase 1 – Environment Preparation

Implemented:

* Laboratory environment planning.
* Virtual machine preparation.
* Network configuration.
* Initial environment validation.

---

## Phase 2 – Wazuh Deployment

Implemented:

* Wazuh Manager installation.
* Wazuh Indexer installation.
* Wazuh Dashboard deployment.
* SIEM platform validation.

---

## Phase 3 – Agent Deployment

Implemented:

* Windows endpoint deployment.
* Wazuh Agent installation.
* Agent registration.
* Communication validation.

---

## Phase 4 – Log Collection

Implemented:

* Windows Event collection.
* Security log ingestion.
* Endpoint telemetry validation.

---

## Phase 5 – Security Monitoring

Implemented:

* Dashboard investigation.
* Event filtering.
* Security event analysis.
* Endpoint activity monitoring.

---

## Phase 6 – Detection Validation

Implemented:

* Authentication monitoring.
* Privileged account activity analysis.
* Security event validation.

Analyzed events:

* Event ID 4624 — Successful Logon.
* Event ID 4672 — Special Privileges Assigned.

---

## Phase 7 – Windows Event Monitoring & PowerShell Detection

Implemented:

* Windows Security Event monitoring.
* Authentication event analysis.
* Privilege monitoring.
* Credential Manager visibility.
* PowerShell Script Block Logging.
* PowerShell command detection.

Detected Windows Events:

* Event ID 4624 — Successful Logon.
* Event ID 4672 — Special Privileges Assigned.
* Event ID 5379 — Credential Manager Access.
* Event ID 4104 — PowerShell Script Block Logging.

PowerShell activity successfully captured:

```powershell
whoami
hostname
Get-Date
Get-WinEvent
```

---

## Phase 8 – MITRE ATT&CK Simulation & Detection Engineering

Implemented:

* Controlled attack simulation.
* PowerShell-based reconnaissance activity.
* Security alert investigation.
* MITRE ATT&CK technique mapping.
* Custom Wazuh rule testing.
* Detection engineering troubleshooting.

Attack simulation:

```powershell
Get-Process
```

MITRE ATT&CK Mapping:

```
T1057 - Process Discovery
```

Detection workflow validated:

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
        ↓
Custom Detection Development
        ↓
Rule Validation
```

Additional activities:

* Creation of custom Wazuh detection rules.
* Testing detection logic through local_rules.xml.
* Troubleshooting Rule ID duplication.
* Validating rule processing.

---

## Phase 9 – Sysmon Integration & Threat Detection

Implemented:

* Microsoft Sysmon deployment.
* Sysmon telemetry validation.
* Wazuh Agent Sysmon integration.
* Windows Sysmon event collection.
* Security event investigation.
* Wazuh detection validation.
* MITRE ATT&CK mapping.

Validated Sysmon channel:

```
Microsoft-Windows-Sysmon/Operational
```

Detection workflow:

```
Sysmon Telemetry
        ↓
Wazuh Agent Collection
        ↓
Wazuh Manager Processing
        ↓
Detection Rule Matching
        ↓
Security Alert Generation
        ↓
MITRE ATT&CK Mapping
```

Detected Sysmon activity:

* Event ID 11 — File Create.

Example detection:

```
Rule ID:
92213

Description:
Executable file dropped in folder commonly used by malware

MITRE ATT&CK:
T1105 - Ingress Tool Transfer
```

---

# Key Findings

The SIEM successfully collected, processed, and analyzed Windows endpoint telemetry.

The laboratory demonstrated:

* Windows Event Log collection.
* PowerShell monitoring.
* Sysmon integration.
* Endpoint telemetry analysis.
* Security alert investigation.
* MITRE ATT&CK mapping.
* Attack simulation.
* Detection engineering.
* Custom rule troubleshooting.

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
│   ├── phase-8-mitre-attack-detection-engineering.md
│   └── phase-9-sysmon-integration-threat-detection.md
│
├── screenshots/
│
└── README.md
```

---

# Documentation

Detailed documentation is available in the **documentation/** directory.

Current documentation:

* Phase 7 – Windows Event Monitoring and PowerShell Detection.
* Phase 8 – MITRE ATT&CK Simulation and Detection Engineering.
* Phase 9 – Sysmon Integration and Threat Detection.

---

# Screenshots

Implementation evidence is stored in the **screenshots/** directory.

Current screenshots include:

* Wazuh Dashboard monitoring.
* Windows authentication events.
* Failed logon detection.
* Privilege-related events.
* PowerShell Event ID 4104.
* Script Block Logging.
* MITRE ATT&CK detection alert.
* Sysmon installation validation.
* Sysmon event ingestion.
* Wazuh Sysmon detection alert.

---

# Skills Demonstrated

## SIEM Operations

* Wazuh administration.
* Event ingestion.
* Log analysis.
* Alert investigation.

## Security Monitoring

* Windows Event Log analysis.
* Authentication monitoring.
* Privilege monitoring.
* Endpoint visibility.
* Sysmon telemetry analysis.

## Threat Detection

* PowerShell activity analysis.
* Script Block Logging.
* Sysmon integration.
* Attack simulation.
* MITRE ATT&CK mapping.
* Detection validation.
* Custom rule development.

## Cybersecurity Concepts

* SIEM architecture.
* Endpoint monitoring.
* Detection engineering.
* Defensive security.
* Blue team operations.
* SOC analyst workflows.

---

# Future Improvements

Planned enhancements include:

* Linux endpoint monitoring.
* Additional Sysmon detection scenarios.
* Custom Wazuh detection rules.
* Atomic Red Team simulations.
* Threat Intelligence integration.
* Active Response automation.
* Sigma rule integration.
* Additional MITRE ATT&CK scenarios.
* Threat hunting exercises.

---

# Conclusion

This project demonstrates the implementation of a functional Wazuh SIEM environment focused on security monitoring, detection validation, threat investigation, and SOC workflows.

The laboratory provides practical experience in deploying a SIEM, monitoring Windows endpoints, collecting security telemetry, integrating Sysmon, investigating alerts, simulating attacker behavior, and developing detection logic.

The project reflects practical SOC analyst activities, including event monitoring, PowerShell analysis, Sysmon investigation, MITRE ATT&CK mapping, and defensive security operations.

**This repository is actively being expanded with additional detection scenarios, attack simulations, and SOC use cases.**