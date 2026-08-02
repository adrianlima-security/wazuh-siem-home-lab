# Wazuh SIEM Home Lab

## Overview

Cybersecurity home lab designed to deploy, configure, and analyze a Security Information and Event Management (SIEM) environment using Wazuh.

The objective of this project is to gain practical experience in security monitoring, endpoint detection, log analysis, and SOC investigation workflows.

---

# Project Objectives

This laboratory was created to develop hands-on skills in:

- SIEM deployment and configuration
- Endpoint monitoring
- Security event collection
- Log analysis
- Alert investigation
- Windows security monitoring
- SOC analyst workflows

---

# Technologies Used

## SIEM Platform

- Wazuh SIEM

## Operating Systems

- Ubuntu Server
- Windows 11 Endpoint

## Security Concepts

- Security Information and Event Management (SIEM)
- Endpoint Detection and Monitoring
- Windows Event Analysis
- Authentication Monitoring
- Security Alert Investigation

---

# Lab Architecture

The environment consists of:

```text
Windows 11 Endpoint
        |
        |
     Wazuh Agent
        |
        |
 Ubuntu Server
(Wazuh Manager + Dashboard)
```

The Windows endpoint sends security events to the Wazuh Manager, where logs are collected, analyzed, and investigated through the dashboard.

---

# Repository Structure

```text
Wazuh-SIEM-Home-Lab/

├── documentation/
│   ├── phase-1-environment-preparation.md
│   ├── phase-2-wazuh-deployment.md
│   ├── phase-3-endpoint-integration.md
│   ├── phase-4-log-collection.md
│   ├── phase-5-detection-analysis.md
│   └── phase-6-security-monitoring.md
│
├── screenshots/
│   ├── phase1/
│   ├── phase2/
│   ├── phase3/
│   ├── phase4/
│   ├── phase5/
│   └── phase6/
│
└── README.md
```

---

# Project Phases

## Phase 1 - Environment Preparation

Completed:

- Lab environment setup
- Virtual machine preparation
- Initial configuration

Documentation:

[Phase 1 - Environment Preparation](documentation/phase-1-environment-preparation.md)

---

## Phase 2 - Wazuh Deployment

Completed:

- Wazuh installation
- Manager deployment
- Dashboard configuration

Documentation:

[Phase 2 - Wazuh Deployment](documentation/phase-2-wazuh-deployment.md)

---

## Phase 3 - Endpoint Integration

Completed:

- Windows 11 endpoint preparation
- Wazuh Agent installation
- Agent registration
- Endpoint communication validation

Documentation:

[Phase 3 - Endpoint Integration](documentation/phase-3-endpoint-integration.md)

---

## Phase 4 - Log Collection Validation

Completed:

- Endpoint log verification
- Event collection testing
- Security data validation

Documentation:

[Phase 4 - Log Collection Validation](documentation/phase-4-log-collection.md)

---

## Phase 5 - Detection and Analysis

Completed:

- Security event review
- Detection validation
- Initial investigation workflow

Documentation:

[Phase 5 - Detection and Analysis](documentation/phase-5-detection-analysis.md)

---

## Phase 6 - Security Monitoring

Completed:

- Agent status verification
- Windows security event monitoring
- Controlled event generation
- Authentication event detection
- Basic alert investigation

Key event analyzed:

```text
Event:
Windows Logon Success

Rule ID:
60106

Severity:
Level 3 - Low

Agent:
lab-win11
```

Documentation:

[Phase 6 - Security Monitoring](documentation/phase-6-security-monitoring.md)

---

# Evidence

Validation screenshots and evidence are stored in:

[screenshots](screenshots/)

Evidence includes:

- Agent connection status
- Security event collection
- Generated authentication events
- Alert investigation workflow

---

# Skills Demonstrated

Through this project, I practiced:

## SIEM

- Wazuh deployment
- Dashboard monitoring
- Security event analysis

## Endpoint Security

- Windows monitoring
- Agent management
- Authentication event investigation

## SOC Operations

- Alert triage
- Event validation
- Basic incident analysis
- Security monitoring workflow

## Cybersecurity Fundamentals

- Log analysis
- Threat detection concepts
- Security event investigation
- Vulnerability assessment concepts

---

# Future Improvements

Planned improvements:

- Add vulnerability scanning integration
- Create custom Wazuh detection rules
- Simulate additional attack scenarios
- Integrate threat intelligence sources
- Expand incident response documentation
- Develop custom detection engineering workflows

---

# Project Status

Current status:

```text
Completed:

✓ Wazuh Deployment
✓ Windows Endpoint Integration
✓ Security Monitoring
✓ Event Investigation

Next:

→ Advanced Detection Engineering
→ Attack Simulation
→ Incident Response Workflows
→ Custom Detection Rules
```

---

# Author

Adrian Lima

Junior Cybersecurity Analyst | SOC | SIEM | Threat Detection

Focused on:

- SOC Operations
- SIEM Monitoring
- Threat Detection
- Security Monitoring
- Vulnerability Assessment