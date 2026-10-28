# Junior SOC Lab Architecture

This document describes the lab architecture for a beginner SOC analyst environment using Wazuh + Elastic Stack.

## Lab purpose

The lab is designed to teach junior analysts how to:

- ingest logs from servers and endpoints
- identify suspicious behavior
- investigate the timeline of activity
- build detections and playbooks
- document security findings

## Topology

### Tier 1: SIEM / Detection Platform

- OS: Ubuntu 22.04+
- Components:
  - Wazuh manager
  - Elastic Stack (Elasticsearch + Kibana)
  - Filebeat or Wazuh agent forwarding
- Responsibilities:
  - collect logs
  - correlate alerts
  - search for suspicious events
  - document detections

### Tier 2: Windows Endpoint

- OS: Windows 10 or Windows Server 2019/2022
- Components:
  - Sysmon
  - Windows Defender
  - PowerShell logging
  - Wazuh agent
- Responsibilities:
  - generate endpoint telemetry
  - simulate execution and persistence activity

### Tier 3: Linux Server

- OS: Ubuntu 22.04+
- Components:
  - SSH logs
  - sudo logs
  - auth logs
  - nginx or apache access logs
  - Wazuh agent
- Responsibilities:
  - simulate privilege escalation and access abuse

### Tier 4: Attack Simulation Host

- OS: Kali Linux or another red-team VM
- Responsibilities:
  - run attack scenarios
  - validate detections
  - test analyst response

## Example network layout

- `10.0.0.10` – Wazuh Manager / SIEM
- `10.0.0.20` – Windows endpoint
- `10.0.0.30` – Linux web server
- `10.0.0.40` – Kali attack box

## Typical event sources

- Authentication logs
- Process creation records
- PowerShell command logs
- Scheduled task creation
- Service creation
- Windows Sysmon event IDs
- Web server access logs
- Sudo and user activity

## Detection focus areas

- brute force activity
- suspicious PowerShell
- user account changes
- software execution from temporary paths
- unusual scheduled tasks
- privilege escalation behavior

## Analyst workflow

1. Receive alert
2. Validate event quality
3. Investigate user, host, and time context
4. Review process and network activity
5. Determine if malicious or benign
6. Escalate and document evidence

## Suggested first lab

Start with a failed login brute force investigation. This gives junior analysts a simple pattern and teaches alert triage quickly.
