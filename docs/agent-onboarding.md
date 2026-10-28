# Wazuh Agent Onboarding Guide

This guide explains how to enroll Windows and Linux endpoints into the Wazuh manager so the SOC lab can collect telemetry.

## Overview

After the Wazuh manager is running, the next step is to install Wazuh agents on:

- the Windows endpoint
- the Linux server

Once installed, the manager begins collecting:

- Windows Security logs
- Sysmon process events
- Linux auth logs
- system logs
- file integrity and command activity where configured

## Prerequisites

- Wazuh manager is installed and reachable
- manager IP is known, for example `10.0.0.10`
- endpoint has outbound connectivity to the manager
- firewall allows the required Wazuh agent ports

## Linux agent installation

Connect to the Ubuntu server and install the Wazuh agent.

```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --dearmor -o /usr/share/keyrings/wazuh.gpg
sudo tee /etc/apt/sources.list.d/wazuh.list > /dev/null <<'EOF'
deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main
EOF

sudo apt-get update
sudo apt-get install -y wazuh-agent
```

Configure the manager address.

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Update the manager IP:

```xml
<client>
  <server>
    <address>10.0.0.10</address>
    <port>1514</port>
    <protocol>tcp</protocol>
  </server>
</client>
```

Then register the agent.

```bash
sudo /var/ossec/bin/agent-auth -m 10.0.0.10
```

Start and enable the service.

```bash
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

Verify the agent status.

```bash
sudo /var/ossec/bin/agent_control -l
```

## Windows agent installation

Download the Wazuh agent installer for Windows. Use the official Wazuh package for the target architecture.

From an administrator PowerShell session:

```powershell
msiexec.exe /i wazuh-agent-4.x.x.msi /qn WAZUH_MANAGER="10.0.0.10" WAZUH_REGISTRATION_SERVER="10.0.0.10" WAZUH_REGISTRATION_PASSWORD=""
```

If the agent is being registered using the default manager password or a custom registration method, adapt the command accordingly for your environment.

Then confirm the service is running.

```powershell
Get-Service -Name WazuhSvc
```

## Enable Sysmon on Windows

Sysmon is a critical logging source for beginner SOC work because it gives process lineage, command execution, and child/parent process visibility.

Download Sysmon from the Sysinternals suite and install it using the default configuration or a simple baseline config.

Example:

```powershell
Sysmon64.exe -i config.xml
```

You can use a minimal config file that captures:

- process creation
- network connections
- remote thread creation
- image load and driver load
- registry events

## Windows logging best practices

Enable the following for the SOC lab:

- PowerShell module logging
- PowerShell script block logging
- Windows Security log collection
- Sysmon process creation logs
- scheduled task creation monitoring

## Validate endpoint enrollment

On the Wazuh manager, check for active agents.

```bash
sudo /var/ossec/bin/agent_control -l
```

In the Wazuh dashboard or Kibana UI, confirm that events from both endpoints are visible.

## Troubleshooting

### Agent is offline

Check the endpoint service:

```bash
sudo systemctl status wazuh-agent
```

On Windows:

```powershell
Get-Service -Name WazuhSvc
```

### Manager not accepting connections

Verify that the manager is listening on port 1514 and the firewall allows traffic.

```bash
sudo ss -lntup | grep 1514
```

### No Windows events in the dashboard

Make sure:

- Wazuh agent is enrolled and connected
- Sysmon is installed and running
- Windows Security log collection is enabled
- the endpoint clock is synchronized

## Best practice for junior analysts

Start by validating these sources first:

- authentication logs
- process creation logs
- PowerShell execution logs
- scheduled task and service creation logs

Those data sources are the foundation for nearly every beginner SOC investigation.
