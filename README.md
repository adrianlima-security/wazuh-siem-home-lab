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

```
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

# Project Phases

## Phase 1 - Environment Preparation

Completed:

- Lab environment setup
- Virtual machine preparation
- Initial configuration

Documentation:

```
documentation/phase-1-environment-preparation.md
```

---

## Phase 2 - Wazuh Deployment

Completed:

- Wazuh installation
- Manager deployment
- Dashboard configuration

Documentation:

```
documentation/phase-2-wazuh-deployment.md
```

---

## Phase 3 - Endpoint Integration

Completed:

- Windows 11 endpoint preparation
- Wazuh Agent installation
- Agent registration
- Endpoint communication validation

Documentation:

```
documentation/phase-3-endpoint-integration.md
```

---

## Phase 4 - Log Collection Validation

Completed:

- Endpoint log verification
- Event collection testing
- Security data validation

Documentation:

```
documentation/phase-4-log-collection.md
```

---

## Phase 5 - Detection and Analysis

Completed:

- Security event review
- Detection validation
- Initial investigation workflow

Documentation:

```
documentation/phase-5-detection-analysis.md
```

---

## Phase 6 - Security Monitoring

Completed:

- Agent status verification
- Windows security event monitoring
- Controlled event generation
- Authentication event detection
- Basic alert investigation

Key event analyzed:

```
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

```
documentation/phase-6-security-monitoring.md
```

---

# Evidence

Screenshots and validation evidence are stored in:

```
screenshots/
```

Examples:

- Agent connection status
- Security events
- Generated activity
- Alert investigation

---

# Skills Demonstrated

Through this project, I practiced:

### SIEM

- Wazuh deployment
- Dashboard monitoring
- Security event analysis

### Endpoint Security

- Windows monitoring
- Agent management
- Authentication event investigation

### SOC Operations

- Alert triage
- Event validation
- Basic incident analysis

### Cybersecurity Fundamentals

- Log analysis
- Threat detection concepts
- Security monitoring workflows

---

# Future Improvements

Planned improvements:

- Add vulnerability scanning integration
- Create custom Wazuh detection rules
- Simulate additional attack scenarios
- Integrate threat intelligence sources
- Expand incident response documentation

---

# Project Status

Current status:

```
Completed:
✓ Wazuh Deployment
✓ Windows Endpoint Integration
✓ Security Monitoring
✓ Event Investigation

Next:
→ Advanced Detection Engineering
→ Attack Simulation
→ Incident Response Workflows
```

---

# Author

Adrian Lima

Cybersecurity Student | Junior Cybersecurity Analyst

Focused on:

- SOC Operations
- SIEM
- Threat Detection
- Security Monitoring
- Vulnerability Assessment