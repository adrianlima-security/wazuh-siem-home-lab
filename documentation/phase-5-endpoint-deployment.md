# Phase 5 - Endpoint Deployment

## Objective

The objective of this phase is to deploy a Wazuh Agent on a Windows 11 endpoint and connect it to the Wazuh Manager running on the Ubuntu Server.

This phase includes agent deployment, service validation, endpoint registration and communication verification with the Wazuh SIEM/XDR platform.

---

# Step 1 - Deploy Wazuh Agent

## Description

A Wazuh Agent was deployed on a Windows 11 endpoint to enable communication with the Wazuh Manager.

The agent deployment wizard was configured from the Wazuh Dashboard.

Configuration:

- Operating System: Windows
- Agent Name: lab-win11
- Wazuh Manager Address: Ubuntu Server IP

The deployment wizard generated the installation command required for the Windows endpoint.

## Evidence

Screenshot:

phase5-01-agent-deployment-wizard.png

---

# Step 2 - Install Wazuh Agent on Windows

## Description

The Wazuh Agent installer was executed on the Windows endpoint using PowerShell with administrator privileges.

Command executed:

    Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.12.0-1.msi -OutFile $env:tmp\wazuh-agent

The MSI installer was executed with the required configuration:

    msiexec.exe /i $env:tmp\wazuh-agent /q WAZUH_MANAGER='SERVER_IP' WAZUH_AGENT_NAME='lab-win11'

## Result

The Wazuh Agent was installed successfully on the Windows endpoint.

---

# Step 3 - Validate Wazuh Agent Service

## Description

After installation, the Windows service was checked to confirm that the Wazuh Agent was correctly installed.

Command executed:

    Get-Service WazuhSvc

Initial status:

    Stopped

The service was started manually:

    Start-Service WazuhSvc

The service status was verified again.

Expected result:

    Running

## Result

The Wazuh Agent service was successfully started.

## Evidence

Screenshot:

phase5-02-agent-service-running.png

---

# Step 4 - Verify Agent Registration

## Description

After starting the service, the Windows endpoint was verified from the Wazuh Dashboard.

The agent appeared with the following configuration:

- Agent Name: lab-win11
- Operating System: Windows 11
- Status: Active

## Result

The Windows endpoint successfully registered with the Wazuh Manager.

Communication between the endpoint and the SIEM platform was confirmed.

## Evidence

Screenshot:

phase5-03-agent-active-dashboard.png

---

# Phase 5 Summary

The Wazuh Agent was successfully deployed on a Windows 11 endpoint and connected to the Wazuh Manager.

Completed tasks:

- Deployed Wazuh Agent on Windows 11.
- Configured communication with Wazuh Manager.
- Installed the Windows service.
- Started and validated the agent service.
- Registered the endpoint successfully.
- Confirmed active communication through the Wazuh Dashboard.

The environment is now ready for security monitoring and event analysis.

---

# Next Phase

The next phase will cover:

- Security event collection.
- Log analysis.
- Alert generation.
- Threat detection validation.
- Wazuh rule and alert investigation.