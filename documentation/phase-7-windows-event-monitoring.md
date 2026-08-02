# Phase 7 - Windows Event Monitoring and PowerShell Detection

## Table of Contents

- Introduction
- Lab Environment
- Phase 7.1 - Monitoring Validation
- Phase 7.2 - Windows Security Event Collection
- Phase 7.3 - PowerShell Monitoring Configuration
- Phase 7.4 - PowerShell Event Validation
- Phase 7.5 - Wazuh PowerShell Detection
- Security Analysis
- Conclusion

---

# Introduction

This document describes the implementation, validation, and analysis performed during Phase 7 of the Wazuh SIEM Home Lab project.

The objective of this phase was to validate that the Wazuh SIEM environment was correctly collecting security telemetry from a Windows endpoint, analyze Windows authentication events, and implement PowerShell monitoring capabilities through Script Block Logging.

This phase simulates a real-world Security Operations Center (SOC) workflow where endpoint activity is collected, centralized, analyzed, and investigated through a SIEM platform.

## Objectives

- Validate communication between the Windows endpoint and Wazuh Manager.
- Confirm successful ingestion of Windows Security Events.
- Analyze authentication-related events.
- Enable PowerShell Script Block Logging.
- Detect and analyze PowerShell execution activity.
- Validate visibility through the Wazuh Dashboard.

---

# Lab Environment

## Wazuh Infrastructure

The SIEM environment consists of:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Ubuntu Server 24.04 LTS

## Monitored Endpoint

Endpoint information:

- Operating System: Windows 11
- Hostname: lab-win11
- Agent: Wazuh Agent

Configured log sources:

- Windows Security Event Log
- Microsoft-Windows-PowerShell/Operational Event Log

---

# Phase 7.1 - Monitoring Validation

Before analyzing security events, the Wazuh Manager configuration and service status were validated.

Configuration test:

```bash
/var/ossec/bin/wazuh-analysisd -t
```

The configuration completed successfully, confirming that no syntax errors were present.

The Wazuh Manager service was restarted:

```bash
systemctl restart wazuh-manager
```

To verify event ingestion from the monitored endpoint, the archive log was monitored:

```bash
tail -f /var/ossec/logs/archives/archives.log
```

The logs confirmed successful communication across the monitoring pipeline.

```text
Windows Endpoint
      │
      ▼
 Wazuh Agent
      │
      ▼
 Wazuh Manager
```

### Evidence

- phase7-01-monitoring-ready.png

---

# Phase 7.2 - Windows Security Event Collection

After confirming communication, Windows Security Events were analyzed.

The Windows endpoint successfully generated multiple security events that were collected and processed by Wazuh.

The primary events analyzed during this phase were:

- **Event ID 4624 – Successful Logon**
- **Event ID 4672 – Special Privileges Assigned to New Logon**
- **Event ID 5379 – Credential Manager Access**

## Event ID 4624 – Successful Logon

Event ID 4624 is generated whenever an account successfully authenticates on a Windows system.

Collected information included:

- User account
- Logon type
- Authentication package
- Source process
- Session details

Example:

```text
Provider: Microsoft-Windows-Security-Auditing
Event ID: 4624
Severity: AUDIT_SUCCESS
```

Authentication events are one of the primary data sources used by SOC analysts to investigate user activity and detect suspicious login behavior.

## Event ID 4672 – Special Privileges Assigned

Event ID 4672 identifies accounts receiving elevated privileges during authentication.

Observed privileges included:

- SeDebugPrivilege
- SeBackupPrivilege
- SeRestorePrivilege
- SeTakeOwnershipPrivilege
- SeImpersonatePrivilege

These privileges are significant because attackers frequently attempt to abuse privileged accounts after gaining initial access to a system.

Monitoring privileged logons helps identify potential privilege escalation and lateral movement activities.

## Event ID 5379 – Credential Manager Access

Event ID 5379 indicates that Windows Credential Manager was accessed.

Potential security implications include:

- Credential theft attempts
- Unauthorized credential access
- Post-exploitation activity

Monitoring credential-related events improves visibility into techniques commonly used after initial compromise.

### Evidence

- phase7-02-failed-login-detection.png
- phase7-03-alert-analysis.png

---

# Phase 7.3 - PowerShell Monitoring Configuration

PowerShell monitoring was enabled to increase endpoint visibility.

PowerShell is frequently leveraged by attackers because it provides powerful administrative and scripting capabilities while being natively available on Windows systems.

To improve detection capabilities, PowerShell Script Block Logging was enabled.

Registry location:

```powershell
HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging
```

Registry key creation:

```powershell
New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Force
```

Enable Script Block Logging:

```powershell
Set-ItemProperty `
-Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" `
-Name EnableScriptBlockLogging `
-Value 1
```

Validation:

```powershell
Get-ItemProperty "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging"
```

Result:

```text
EnableScriptBlockLogging : 1
```

This configuration enables Windows to record executed PowerShell commands as Event ID 4104, significantly improving visibility during security investigations.

---

# Phase 7.4 - PowerShell Event Validation

After enabling Script Block Logging, PowerShell activity was generated and validated.

Executed command:

```powershell
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational" -MaxEvents 20 | Select Id, TimeCreated, Message
```

The endpoint generated several PowerShell Operational events, including:

- **Event ID 40961 – PowerShell Console Starting**
- **Event ID 40962 – PowerShell Console Ready**
- **Event ID 53504 – IPC Thread Started**
- **Event ID 4104 – Script Block Logging**

## Event ID 4104 – PowerShell Script Block Logging

Event ID 4104 records the content of executed PowerShell commands.

Examples captured during testing:

```powershell
whoami
hostname
Get-Date
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational"
```

PowerShell monitoring provides valuable visibility into attacker behavior.

Common malicious use cases include:

- System discovery
- Credential access
- Downloading payloads
- Malicious script execution
- Persistence mechanisms
- Living-off-the-Land (LotL) techniques

Capturing Event ID 4104 enables analysts to reconstruct attacker activity by recording executed PowerShell commands.

### Evidence

- phase7-04-powershell-event.png
- phase7-05-powershell-scriptblock-4104.png

---

# Phase 7.5 - Wazuh PowerShell Detection

After enabling PowerShell logging, event ingestion was validated on the Wazuh Manager.

Command used:

```bash
grep -i "PowerShell" /var/ossec/logs/archives/archives.log
```

The output confirmed successful ingestion of PowerShell events generated on the Windows endpoint.

Collected information included:

- Provider name
- Event ID
- Script Block content
- Timestamp
- Hostname
- Executed commands

Examples detected:

```powershell
whoami
hostname
Get-Date
```

The complete monitoring pipeline was successfully validated.

```text
Windows Endpoint
      │
      ▼
 Wazuh Agent
      │
      ▼
 Wazuh Manager
      │
      ▼
 Wazuh Dashboard
```

### Evidence

- phase7-06-wazuh-dashboard-powershell-alert.png

---

# Security Analysis

During this phase, the Wazuh SIEM successfully collected, processed, and analyzed Windows endpoint telemetry.

## Authentication Monitoring

Capabilities:

- Successful logon detection
- Privileged authentication monitoring
- Credential access visibility

Security benefits:

- Detection of suspicious login activity
- Investigation of user behavior
- Identification of privileged account usage
- Detection of potential privilege escalation

From a SOC perspective, authentication events represent one of the primary sources used during incident investigations. Correlating authentication activity allows analysts to identify abnormal behavior, unauthorized access, and account compromise.

## PowerShell Monitoring

Capabilities:

- PowerShell command visibility
- Script Block Logging
- User activity tracking
- Command execution history

Security benefits:

- Detection of suspicious scripts
- Investigation of attacker behavior
- Identification of Living-off-the-Land techniques
- Increased endpoint visibility

PowerShell remains one of the most common tools abused by attackers due to its native availability and administrative capabilities. Capturing Event ID 4104 significantly improves detection by recording executed commands, allowing analysts to reconstruct attacker activity and identify potentially malicious scripts.

---

# Conclusion

Phase 7 successfully validated end-to-end Windows event monitoring using Wazuh SIEM.

The environment demonstrated complete visibility from endpoint activity generation to centralized collection, processing, analysis, and investigation within the SIEM platform.

The following objectives were achieved:

- Windows endpoint successfully connected to Wazuh.
- Windows Security Events were collected and analyzed.
- Authentication events were monitored.
- PowerShell Script Block Logging was enabled.
- PowerShell execution activity was successfully detected.
- Events were visualized and investigated through the Wazuh Dashboard.

This phase demonstrates practical SOC analyst skills including SIEM administration, event investigation, Windows log analysis, endpoint monitoring, PowerShell detection, and defensive security operations.

The implementation also establishes a solid foundation for future phases involving detection engineering, custom Wazuh rules, threat hunting, attack simulations, and incident response workflows.