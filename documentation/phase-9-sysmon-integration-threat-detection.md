# Phase 9 – Sysmon Integration & Threat Detection

## Overview

This phase documents the integration of Microsoft Sysmon with the Wazuh SIEM environment to improve endpoint visibility and enhance threat detection capabilities.

The objective was to deploy Sysmon on the Windows endpoint (`lab-win11`), collect Sysmon telemetry through the Wazuh Agent, validate event ingestion, and analyze security detections mapped to the MITRE ATT&CK framework.

Sysmon provides detailed endpoint telemetry such as process creation, file creation, network connections, and other system activities that are valuable for Security Operations Center (SOC) investigations.

---

# Objectives

* Install and configure Microsoft Sysmon on the Windows endpoint.
* Enable Sysmon event collection through Wazuh Agent.
* Validate Microsoft-Windows-Sysmon/Operational log ingestion.
* Investigate Sysmon-generated security events.
* Analyze Wazuh detections generated from Sysmon telemetry.
* Validate MITRE ATT&CK technique mapping.

---

# Environment

## SIEM

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

# Sysmon Installation

Microsoft Sysmon was installed on the Windows endpoint to provide enhanced security telemetry.

Installation files included:

```
Sysmon.exe
Sysmon64.exe
sysmonconfig-export.xml
```

The Sysmon service was successfully installed and started on the endpoint.

---

# Sysmon Event Validation

Before integrating with Wazuh, Sysmon event generation was validated locally on Windows.

The following PowerShell command was used:

```powershell
Get-WinEvent -ListLog *Sysmon*
```

Output confirmed the presence of:

```
Microsoft-Windows-Sysmon/Operational
```

Sysmon events were successfully generated and visible through Windows Event Viewer.

---

# Wazuh Agent Configuration

The Wazuh Agent configuration file was updated to collect Sysmon events.

Configuration file:

```
C:\Program Files (x86)\ossec-agent\ossec.conf
```

Added event channel:

```xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

After modifying the configuration, the Wazuh Agent service was restarted:

```powershell
Restart-Service WazuhSvc
```

---

# Troubleshooting

## Issue: Sysmon Channel Not Initially Loaded

After the first restart, the Wazuh Agent logs showed PowerShell event collection but did not show Sysmon:

Initial state:

```
Analyzing event log:
Microsoft-Windows-PowerShell/Operational
```

The Sysmon event channel was not being monitored.

## Resolution

The Sysmon configuration entry was reviewed and corrected inside `ossec.conf`.

After restarting the Wazuh Agent, the following confirmation appeared:

```
Analyzing event log:
Microsoft-Windows-Sysmon/Operational
```

This confirmed successful integration between Sysmon and Wazuh Agent.

---

# Event Ingestion Validation

A validation event was generated from the Windows endpoint.

The Wazuh Dashboard successfully received Sysmon telemetry.

Confirmed fields:

```
agent.name:
lab-win11

data.win.system.providerName:
Microsoft-Windows-Sysmon

data.win.system.channel:
Microsoft-Windows-Sysmon/Operational
```

This confirmed the complete telemetry pipeline:

```
Windows Endpoint
        |
        |
      Sysmon
        |
        |
 Wazuh Agent
        |
        |
 Wazuh Manager
        |
        |
 Wazuh Dashboard
```

---

# Detection Analysis

A Sysmon Event ID 11 was detected.

Event:

```
Sysmon Event ID 11
File Create
```

Detected activity:

```
Image:
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

Created file:

```
C:\Users\adria\AppData\Local\Temp\__PSScriptPolicyTest_qt45cguh.4qi.ps1
```

User:

```
Adrian\Adrian
```

---

# Wazuh Detection

The event was automatically analyzed by Wazuh rules.

Detection:

```
Rule ID:
92213
```

Description:

```
Executable file dropped in folder commonly used by malware
```

Severity:

```
Level 15
```

The alert demonstrated that Wazuh was not only collecting Sysmon telemetry but also applying detection logic to identify suspicious behavior.

---

# MITRE ATT&CK Mapping

The alert was automatically mapped to MITRE ATT&CK.

Technique:

```
T1105 - Ingress Tool Transfer
```

Tactic:

```
Command and Control
```

This demonstrates the integration between endpoint telemetry, SIEM detection rules, and threat intelligence frameworks.

---

# Skills Demonstrated

## Endpoint Monitoring

* Microsoft Sysmon deployment
* Windows event analysis
* Endpoint telemetry collection

## SIEM Operations

* Wazuh Agent configuration
* Event ingestion validation
* Alert investigation

## Threat Detection

* Sysmon event analysis
* Detection rule validation
* MITRE ATT&CK mapping

## SOC Analyst Workflow

* Log source onboarding
* Troubleshooting collection issues
* Investigating security alerts
* Mapping detections to adversary techniques

---

# Screenshots

Evidence collected:

```
phase-9-01-sysmon-installation.png
phase-9-02-sysmon-event-validation.png
phase-9-03-wazuh-agent-sysmon-integration.png
phase-9-04-sysmon-event-ingestion.png
phase-9-05-sysmon-wazuh-mitre-detection.png
```

---

# Conclusion

This phase successfully integrated Microsoft Sysmon with the Wazuh SIEM environment.

The laboratory now provides enhanced endpoint visibility through Sysmon telemetry, enabling deeper investigation of Windows activity and improving detection capabilities.

The successful ingestion of Sysmon events, Wazuh alert generation, and MITRE ATT&CK mapping demonstrate a realistic SOC monitoring workflow.

This implementation represents practical experience with endpoint detection, SIEM operations, and defensive security monitoring.