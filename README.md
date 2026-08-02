# Wazuh SIEM Home Lab

![Platform](https://img.shields.io/badge/Platform-Wazuh-blue)
![OS](https://img.shields.io/badge/OS-Ubuntu%2024.04%20%7C%20Windows%2011-green)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)
![License](https://img.shields.io/badge/Project-Home%20Lab-red)

---

## Overview

This project documents the implementation of a Wazuh SIEM Home Lab designed to simulate a Security Operations Center (SOC) monitoring environment.

The objective is to gain hands-on experience with SIEM deployment, endpoint monitoring, Windows Event Log collection, PowerShell monitoring, alert investigation, and SOC analyst workflows.

The laboratory reproduces a real-world defensive security environment where endpoint telemetry is collected, analyzed, and investigated through a centralized SIEM platform.

---

## Objectives

- Deploy a functional Wazuh SIEM environment.
- Configure endpoint monitoring.
- Collect Windows security events.
- Investigate authentication activity.
- Monitor PowerShell execution.
- Analyze security alerts.
- Practice SOC investigation workflows.
- Develop practical blue team skills.

---

## Lab Architecture

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
       Security Event Investigation
```

---

## Environment

### SIEM Platform

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

### Server

- Ubuntu Server 24.04 LTS

### Endpoint

- Windows 11
- Wazuh Agent

---

## Technologies Used

### Security

- Wazuh SIEM
- Windows Event Logs
- PowerShell Script Block Logging
- Security Monitoring
- Endpoint Detection & Response (EDR) Concepts

### Infrastructure

- Ubuntu Server
- Windows 11 Virtual Machine
- Git
- GitHub

---

## Project Phases

### Phase 1 – Environment Preparation

- Server deployment
- Initial configuration
- Network validation

### Phase 2 – Wazuh Deployment

- Installed Wazuh Manager
- Installed Wazuh Indexer
- Installed Wazuh Dashboard

### Phase 3 – Agent Deployment

- Installed Wazuh Agent
- Connected Windows endpoint
- Validated communication

### Phase 4 – Log Collection

- Windows Event collection
- Security log ingestion
- Endpoint telemetry validation

### Phase 5 – Security Monitoring

- Alert analysis
- Event filtering
- Dashboard investigation

### Phase 6 – Detection Validation

- Authentication monitoring
- Privileged account activity
- Security event validation

### Phase 7 – Windows Event Monitoring & PowerShell Detection

Implemented:

- Windows Security Event monitoring
- Authentication event analysis
- Privilege monitoring
- Credential Manager visibility
- PowerShell Script Block Logging
- PowerShell command detection

Detected Windows Events:

- Event ID 4624 — Successful Logon
- Event ID 4672 — Special Privileges Assigned
- Event ID 5379 — Credential Manager Access
- Event ID 4104 — PowerShell Script Block Logging

---

## Key Findings

The SIEM successfully collected, processed, and displayed Windows endpoint telemetry.

PowerShell Script Block Logging was enabled, allowing Wazuh to capture executed PowerShell commands, including:

- `whoami`
- `hostname`
- `Get-Date`
- `Get-WinEvent`

Authentication events and privilege-related activity were successfully ingested into the SIEM, demonstrating end-to-end visibility from the Windows endpoint to the Wazuh Dashboard.

---

## Repository Structure

```
wazuh-siem-home-lab/
│
├── documentation/
│   └── phase-7-windows-event-monitoring.md
│
├── screenshots/
│
└── README.md
```

---

## Documentation

Detailed documentation is available in the **documentation/** directory.

Current documentation:

- Phase 7 – Windows Event Monitoring and PowerShell Detection

---

## Screenshots

Implementation evidence is stored in the **screenshots/** directory.

Current screenshots include:

- Monitoring validation
- Failed logon detection
- Alert investigation
- PowerShell Event ID 4104
- Script Block Logging
- Wazuh Dashboard investigation

---

## Skills Demonstrated

### SIEM Operations

- Wazuh administration
- Event ingestion
- Log analysis
- Alert investigation

### Security Monitoring

- Windows Event Log analysis
- Authentication monitoring
- Privilege monitoring
- Endpoint visibility

### Threat Detection

- PowerShell activity analysis
- Script Block Logging
- Suspicious activity investigation
- SOC investigation workflow

### Cybersecurity Concepts

- SIEM architecture
- Endpoint monitoring
- Detection engineering
- Defensive security
- Security Operations Center (SOC) workflows

---

## Future Improvements

Planned enhancements include:

- Linux endpoint monitoring
- Sysmon integration
- Custom Wazuh detection rules
- Attack simulations (Atomic Red Team)
- Threat Intelligence integration
- Active Response automation
- MITRE ATT&CK mapping
- Sigma rule integration

---

## Conclusion

This project demonstrates the implementation of a functional Wazuh SIEM environment for security monitoring and event investigation.

The laboratory provides practical experience in deploying a SIEM, monitoring Windows endpoints, collecting security telemetry, investigating alerts, and validating detection capabilities.

The project reflects practical SOC analyst activities, including event monitoring, PowerShell analysis, authentication investigation, and defensive security operations.

**This repository is actively being expanded with additional detection scenarios, attack simulations, and SOC use cases.**