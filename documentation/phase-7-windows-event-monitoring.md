# Phase 7 - Windows Event Monitoring and PowerShell Detection

## Introduction

This document describes the implementation, validation, and analysis process performed during Phase 7 of the Wazuh SIEM Home Lab project.

The objective of this phase was to validate that the Wazuh SIEM environment was correctly collecting security telemetry from a Windows endpoint, analyze Windows authentication events, and implement PowerShell monitoring capabilities through Script Block Logging.

This phase represents a realistic Security Operations Center (SOC) workflow, where endpoint activity is collected, centralized, analyzed, and investigated through a SIEM platform.

The main objectives were:

- Validate communication between the Windows endpoint and Wazuh Manager.
- Confirm successful ingestion of Windows Security Events.
- Analyze authentication-related events.
- Enable PowerShell Script Block Logging.
- Detect and analyze PowerShell execution activity.
- Validate visibility through Wazuh Dashboard.


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
- Agent Type: Wazuh Agent

The monitored sources configured on the endpoint include:

- Windows Security Event Log
- Microsoft-Windows-PowerShell/Operational Event Log


# Phase 7.1 - Monitoring Validation

Before analyzing security events, the Wazuh Manager configuration and service status were validated.

The configuration test was executed using:
/var/ossec/bin/wazuh-analysisd -t


The command completed successfully, confirming that the Wazuh Manager configuration was valid.

The manager service was restarted:
systemctl restart wazuh-manager

After restarting the service, the archive log was monitored to verify that events were being received from the Windows endpoint.

Command used:
tail -f /var/ossec/logs/archives/archives.log


The logs confirmed successful communication between:

Windows Endpoint → Wazuh Agent → Wazuh Manager


Evidence:

- phase7-01-monitoring-ready.png


# Phase 7.2 - Windows Security Event Collection

After confirming communication, Windows security events were analyzed.

The Windows endpoint successfully generated multiple security events that were collected by Wazuh.

The main events analyzed were:

- Event ID 4624 - Successful Logon
- Event ID 4672 - Special Privileges Assigned to New Logon
- Event ID 5379 - Credential Manager Access


## Event ID 4624 - Successful Logon

Event ID 4624 is generated when an account successfully authenticates on the Windows system.

The collected information included:

- Account information
- Logon type
- Authentication package
- Process responsible for creating the session

Example:
Event ID: 4624
Provider: Microsoft-Windows-Security-Auditing
Severity: AUDIT_SUCCESS


This event is important because authentication monitoring is one of the main detection sources in a SOC environment.


## Event ID 4672 - Privileged Logon

Event ID 4672 identifies accounts receiving special privileges during authentication.

Detected privileges included:

- SeDebugPrivilege
- SeBackupPrivilege
- SeRestorePrivilege
- SeTakeOwnershipPrivilege
- SeImpersonatePrivilege


These privileges are relevant because attackers may attempt to abuse elevated permissions after gaining access to a system.


## Event ID 5379 - Credential Manager Access

Event ID 5379 indicates that stored credentials from Windows Credential Manager were accessed.

This type of event is relevant for detecting credential-related activity.

Potential security implications include:

- Credential theft attempts
- Unauthorized access
- Post-exploitation activity


Evidence:

- phase7-02-failed-login-detection.png
- phase7-03-alert-analysis.png


# Phase 7.3 - PowerShell Monitoring Configuration

PowerShell monitoring was enabled to increase endpoint visibility.

PowerShell is frequently used by attackers because it provides powerful scripting capabilities and can execute commands directly on Windows systems.

To improve detection capabilities, Script Block Logging was enabled.


The registry location configured was:
HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging


The registry key was created using:
New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Force


Script Block Logging was enabled:
Set-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging"
-Name EnableScriptBlockLogging `
-Value 1


The configuration was validated:
Get-ItemProperty "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging"


Validation result:
EnableScriptBlockLogging : 1


This configuration allows Windows to generate detailed PowerShell execution logs.


# Phase 7.4 - PowerShell Event Validation

After enabling Script Block Logging, PowerShell events were generated and validated.

The following command was executed:
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational" -MaxEvents 20 | Select Id, TimeCreated, Message

The endpoint generated several PowerShell events:

- Event ID 40961 - PowerShell Console Starting
- Event ID 40962 - PowerShell Console Ready
- Event ID 53504 - PowerShell IPC Thread
- Event ID 4104 - Script Block Logging


The most relevant event was Event ID 4104.


# Event ID 4104 - PowerShell Script Block Logging

Event ID 4104 records the content of PowerShell commands executed on the endpoint.

Examples detected:
whoami

hostname

Get-Date

Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational"

This information provides valuable visibility for detecting malicious PowerShell usage.

Common attacker activities involving PowerShell include:

- System discovery
- Credential access
- Downloading payloads
- Execution of malicious scripts
- Persistence techniques


Evidence:

- phase7-04-powershell-event.png
- phase7-04-powershell-scriptblock-4104.png


# Phase 7.5 - Wazuh PowerShell Detection

After enabling PowerShell logging, events were verified on the Wazuh Manager.

The following command was used:
grep -i "PowerShell" /var/ossec/logs/archives/archives.log

The output confirmed successful ingestion of PowerShell events from the Windows endpoint.

Detected information included:

- PowerShell provider
- Event ID
- ScriptBlock content
- Timestamp
- Endpoint hostname


Example:
Creating Scriptblock text:

whoami

hostname

Get-Date

The complete event flow was validated:
Windows Endpoint
|
|
Wazuh Agent
|
|
Wazuh Manager
|
|
Wazuh Dashboard


Evidence:

- phase7-05-wazuh-dashboard-powershell-alert.png


# Security Analysis

During this phase, the Wazuh SIEM demonstrated the ability to collect and analyze endpoint telemetry.

The implemented monitoring capabilities provide visibility into:


## Authentication Monitoring

Capabilities:

- Successful logon detection
- Privileged authentication detection
- Credential access monitoring


Security benefits:

- Identification of suspicious authentication behavior
- Investigation of account activity
- Detection of potential privilege abuse


## PowerShell Monitoring

Capabilities:

- Command execution visibility
- Script Block analysis
- User activity tracking


Security benefits:

- Detection of suspicious scripts
- Investigation of attacker behavior
- Identification of living-off-the-land techniques


# Conclusion

Phase 7 successfully validated Windows endpoint monitoring using Wazuh SIEM.

The environment demonstrated complete visibility from endpoint activity generation to centralized SIEM analysis.

The following objectives were achieved:

- Windows endpoint successfully connected to Wazuh.
- Security events were collected and analyzed.
- Authentication events were monitored.
- PowerShell Script Block Logging was enabled.
- PowerShell execution activity was detected.
- Events were visualized and investigated through Wazuh Dashboard.

This phase demonstrates practical SOC analyst skills including SIEM monitoring, event investigation, endpoint detection, and security log analysis.