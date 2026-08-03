# Phase 8: MITRE ATT&CK Simulation & Detection Validation

## Objective

The objective of this phase was to simulate an attacker technique based on the MITRE ATT&CK framework and validate Wazuh's ability to detect, classify, and generate security alerts from endpoint activity.

This exercise focused on performing a controlled PowerShell-based attack simulation on a Windows endpoint, collecting the generated telemetry, analyzing the resulting Wazuh alert, and mapping the detected behavior to a MITRE ATT&CK technique.

---

# 8.1 Attack Simulation

A controlled attack simulation was performed on the Windows endpoint:

**Endpoint:**

```
lab-win11
```

The simulated activity represented attacker behavior after gaining access to a Windows system.

PowerShell was used to execute a process discovery command:

```powershell
Get-Process
```

The purpose of this activity was to simulate reconnaissance behavior where an attacker attempts to identify running processes within the compromised environment.

Process enumeration can help attackers discover:

* Running applications
* Security tools
* System processes
* Potential targets for further exploitation

---

# 8.2 MITRE ATT&CK Technique Mapping

The simulated activity was mapped to the MITRE ATT&CK framework.

## Technique

```
T1057 - Process Discovery
```

## Description

Process Discovery allows attackers to identify processes running on a compromised system.

Adversaries may use this information to understand the environment, identify security software, or determine possible next steps during an intrusion.

---

# 8.3 Windows Telemetry Collection

The activity generated Windows PowerShell telemetry through:

```
Microsoft-Windows-PowerShell/Operational
```

The relevant Windows event collected was:

```
Event ID: 4104
```

Event ID 4104 corresponds to PowerShell Script Block Logging, which records PowerShell command content and provides visibility into executed scripts.

The telemetry flow was:

```
Windows Endpoint
        |
        |
PowerShell Activity
        |
        |
Windows Event Log (Event ID 4104)
        |
        |
Wazuh Agent
        |
        |
Wazuh Manager
        |
        |
Security Alert Generated
```

---

# 8.4 Wazuh Detection

After executing the simulated activity, Wazuh successfully collected and analyzed the generated events.

The alert generated contained the following information:

```
Agent:
lab-win11

Rule ID:
91815

Rule Level:
4

MITRE Technique:
T1057 - Process Discovery
```

The Wazuh alert identified the activity as PowerShell process discovery behavior.

---

# 8.5 Alert Investigation

The generated alert was investigated through the Wazuh Dashboard.

The investigation process included:

* Identifying the affected endpoint.
* Reviewing the timestamp of the event.
* Analyzing the PowerShell command execution.
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

MITRE ATT&CK:
T1057 - Process Discovery
```

---

# 8.6 Detection Workflow Demonstrated

This exercise demonstrated a simplified SOC analyst workflow:

```
Attack Simulation
        |
        ↓
Telemetry Generation
        |
        ↓
Log Collection
        |
        ↓
SIEM Analysis
        |
        ↓
Detection Rule Matching
        |
        ↓
MITRE ATT&CK Classification
        |
        ↓
Security Investigation
```

---

# 8.7 Key Findings

During this phase, the following capabilities were validated:

* Wazuh Agent successfully collected endpoint telemetry.
* Windows PowerShell activity was visible through event logging.
* Wazuh detection rules identified suspicious behavior.
* Alerts contained MITRE ATT&CK classification.
* The investigation process provided visibility into attacker techniques.

---

# 8.8 Lessons Learned

This phase provided practical experience with:

* Simulating attacker behavior in a controlled environment.
* Understanding how endpoint activity becomes security telemetry.
* Investigating SIEM alerts.
* Using MITRE ATT&CK as a framework for classifying adversary techniques.
* Following a SOC-style detection and investigation workflow.

This exercise represents a transition from basic SIEM deployment into practical security monitoring and detection engineering.

---

# Conclusion

The MITRE ATT&CK simulation successfully demonstrated the ability of the Wazuh SIEM/XDR platform to detect endpoint activity, generate actionable alerts, and provide context for security investigations.

By combining endpoint telemetry, SIEM analysis, and MITRE ATT&CK mapping, this phase recreated a simplified real-world SOC detection scenario.