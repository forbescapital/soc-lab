# Environment Setup Guide

This guide describes how to build the beginner SOC lab environment in a small home or classroom setup.

## Prerequisites

You will need the following:

- 4 virtual machines or containers
- virtualization software such as VMware, VirtualBox, or Proxmox
- enough RAM for the lab (minimum 16 GB recommended)
- a private lab network or NAT network
- admin access to each VM

## Recommended VM sizing

- SIEM server: 4 vCPU, 8 GB RAM
- Windows endpoint: 2 vCPU, 4 GB RAM
- Linux server: 2 vCPU, 4 GB RAM
- Kali: 2 vCPU, 4 GB RAM

## Step 1: Create the lab network

Create a private internal network for the lab environment.

Suggested subnet:

- 10.0.0.0/24

Assign addresses:

- SIEM: 10.0.0.10
- Windows endpoint: 10.0.0.20
- Linux server: 10.0.0.30
- Kali attacker: 10.0.0.40

## Step 2: Deploy the SIEM server

Install Ubuntu 22.04 on the SIEM host.

Then install and configure:

- Wazuh manager
- Elasticsearch
- Kibana
- Filebeat

Basic checklist:

- ensure host time is synchronized
- enable SSH
- open required ports for agent communication
- install certificates if required by your configuration

## Step 3: Deploy the Windows endpoint

Install Windows 10/11 or Windows Server 2019/2022.

Enable:

- PowerShell logging
- task manager and process monitoring
- Sysmon
- Windows Security log collection
- Wazuh agent

Recommended logging:

- Security log enabled
- PowerShell module and script logging enabled
- Sysmon process creation logging enabled

## Step 4: Deploy the Linux server

Install Ubuntu 22.04 and configure:

- SSH access
- sudo logs
- auth logs
- nginx or Apache access logs
- Wazuh agent

Verify:

- `/var/log/auth.log` is being collected
- SSH access attempts can be observed
- sudo activity is visible

## Step 5: Deploy the Kali attack VM

Install Kali Linux and keep it isolated from production or outside networks.

Use it to test:

- password spraying
- brute-force login attempts
- process execution
- malicious script execution

## Step 6: Validate log ingestion

On the SIEM, confirm the following:

- Windows endpoint is sending Security and Sysmon logs
- Linux server is sending auth and system logs
- agent status is healthy
- events appear in the dashboard or search view

## Step 7: Run the starter labs

Begin with:

- failed SSH logins
- suspicious PowerShell execution

## Troubleshooting

If logs are missing:

- confirm the agent service is running
- check time sync settings
- verify firewall rules
- review certificates or trust configuration
- confirm the client is communicating with the Wazuh manager

## Suggested next steps

- add alert rules and dashboards
- configure detection baselines
- create false positive reviews
- run more advanced attack scenarios
