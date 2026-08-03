# Phase 8: MITRE ATT&CK Simulation & Detection Engineering

## Objective

The objective of this phase was to simulate attacker behavior based on the MITRE ATT&CK framework and validate Wazuh's detection capabilities through endpoint telemetry analysis, alert investigation, and custom detection engineering.

This phase introduced a complete SOC workflow:

```
Attack Simulation
        ↓
Telemetry Collection
        ↓
SIEM Detection
        ↓
Alert Investigation
        ↓
Detection Engineering
```

The goal was to understand how attacker activity generates security telemetry, how Wazuh detects suspicious behavior, and how custom detection logic can be developed and validated.

---

# 8.1 Attack Simulation

A controlled attack simulation was performed against the Windows endpoint.

## Endpoint

```
lab-win11
```

The simulated activity represented attacker reconnaissance behavior by enumerating running processes on a Windows system using PowerShell.

Command executed:

```powershell
Get-Process
```

The purpose of this activity was to simulate how an attacker may gather information about a compromised system after gaining access.

Process discovery can help identify:

* Running applications.
* Security software.
* System processes.
* Potential targets for further actions.

---

# 8.2 MITRE ATT&CK Mapping

The simulated activity was mapped to the MITRE ATT&CK framework.

## Technique

```
T1057 - Process Discovery
```

## Description

Process Discovery allows adversaries to identify processes running on a compromised system.

Attackers may use this information to understand the environment, identify security tools, and determine possible next steps during an intrusion.

---

# 8.3 PowerShell Telemetry Collection

PowerShell activity was monitored through Windows event logging.

Log source:

```
Microsoft-Windows-PowerShell/Operational
```

Relevant Windows Event:

```
Event ID 4104 - PowerShell Script Block Logging
```

PowerShell Script Block Logging provided visibility into executed PowerShell commands and allowed Wazuh to analyze endpoint activity.

Telemetry flow:

```
Windows 11 Endpoint
        ↓
PowerShell Execution
        ↓
Windows Event Log (Event ID 4104)
        ↓
Wazuh Agent
        ↓
Wazuh Manager
        ↓
Security Alert
```

---

# 8.4 Wazuh Detection

After executing the simulated activity, Wazuh successfully collected and analyzed the generated telemetry.

The alert generated contained the following information:

```
Agent:
lab-win11

Rule ID:
91815

Rule Level:
4

MITRE ATT&CK:
T1057 - Process Discovery
```

Detection:

```
PowerShell executing process discovery activity
```

The alert demonstrated that Wazuh was able to identify suspicious endpoint behavior and associate the activity with a known MITRE ATT&CK technique.

---

# 8.5 Alert Investigation

The generated alert was investigated through the Wazuh Dashboard.

The investigation process included:

* Identifying the affected endpoint.
* Reviewing the event timestamp.
* Analyzing the PowerShell activity.
* Validating the detection rule.
* Confirming the MITRE ATT&CK classification.

Evidence collected:

```
Agent Name:
lab-win11

Event Source:
Microsoft-Windows-PowerShell/Operational

Event ID:
4104

Rule ID:
91815

MITRE ATT&CK Technique:
T1057 - Process Discovery
```

---

# 8.6 Detection Engineering and Custom Rule Testing

During this phase, additional detection engineering activities were performed.

A custom Wazuh rule was created to understand how detection logic can be extended beyond the default rule set.

Configuration file:

```
/var/ossec/etc/rules/local_rules.xml
```

Custom Rule:

```
Rule ID:
100001
```

The objective was to create and test custom detection logic based on collected endpoint telemetry.

---

# 8.7 Troubleshooting Custom Rule Duplication

During custom rule validation, a rule ID duplication issue was identified.

The duplicated Rule ID caused conflicts during Wazuh rule processing.

Troubleshooting steps included:

* Reviewing the local_rules.xml configuration.
* Identifying duplicated rule definitions.
* Adjusting custom rule configuration.
* Restarting Wazuh services.
* Validating rule processing.

This troubleshooting process demonstrated practical SIEM administration and detection engineering skills.

Understanding rule conflicts and correcting configuration issues is an essential skill when managing production detection environments.

---

# 8.8 SOC Workflow Demonstrated

This phase demonstrated a simplified SOC analyst workflow:

```
Attack Simulation
        ↓
Endpoint Telemetry Generation
        ↓
Log Collection
        ↓
SIEM Analysis
        ↓
Detection Rule Matching
        ↓
Alert Investigation
        ↓
MITRE ATT&CK Classification
        ↓
Custom Detection Development
        ↓
Rule Validation
```

---

# 8.9 Lessons Learned

This phase provided hands-on experience with:

* MITRE ATT&CK technique mapping.
* PowerShell monitoring.
* Windows Event Log analysis.
* SIEM alert investigation.
* Detection engineering concepts.
* Custom Wazuh rule development.
* Troubleshooting SIEM configurations.
* SOC analyst workflows.

---

# Conclusion

This phase demonstrated how a SOC analyst can move from passive security monitoring into active detection engineering.

By combining attack simulation, endpoint telemetry analysis, MITRE ATT&CK mapping, alert investigation, and custom rule development, the Wazuh Home Lab evolved into a practical security monitoring and detection environment.

This exercise represents a realistic defensive security workflow where attacker behavior is simulated, detected, analyzed, and transformed into actionable security intelligence.