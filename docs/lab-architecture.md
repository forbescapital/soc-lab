# Junior SOC Lab Architecture

This document explains the beginner SOC environment used in this repository.

## Goal

Build a small but realistic SOC lab that teaches junior analysts the core functions of a modern security operations team.

## Lab topology

### 1. SIEM / Monitoring Platform

- Host: Ubuntu 22.04+
- Components:
  - Wazuh Manager
  - Elasticsearch
  - Kibana
  - Filebeat or Wazuh agent collection
- Purpose:
  - collect logs from endpoints and servers
  - correlate alerts and detections
  - support search, triage, and investigation

### 2. Windows Endpoint

- Host: Windows 10/11 or Server 2019/2022
- Components:
  - Sysmon
  - Windows Security logs
  - PowerShell logging
  - Microsoft Defender
  - Wazuh agent
- Purpose:
  - generate process execution events
  - show suspicious PowerShell, parent-child process chains, and service activity

### 3. Linux Server

- Host: Ubuntu 22.04+
- Components:
  - SSH daemon logs
  - auth.log and syslog
  - sudo logs
  - nginx or apache access logs
  - Wazuh agent
- Purpose:
  - simulate failed logins and account abuse
  - generate realistic authentication and system activity

### 4. Red Team / Attack VM

- Host: Kali Linux or another attacker VM
- Purpose:
  - brute-force credentials
  - run suspicious PowerShell commands
  - validate detections and false positives

## Example network

- 10.0.0.10 — SIEM server
- 10.0.0.20 — Windows endpoint
- 10.0.0.30 — Linux server
- 10.0.0.40 — Attack box

## Event sources

- Windows Security Event Log
- Sysmon process events
- PowerShell operational logs
- Linux authentication logs
- SSH failed login attempts
- sudo usage logs
- web server access logs
- scheduled task and service creation logs

## Alert categories

- brute force activity
- suspicious process execution
- unusual PowerShell execution
- persistence via registry, service, or scheduled task
- privilege escalation paths
- suspicious login patterns

## Typical analyst workflow

1. Receive an alert
2. Validate the impacted host and user
3. Inspect the time window and attacker source
4. Review relevant logs and endpoint events
5. Determine whether the activity is malicious
6. Escalate or document the findings

## Suggested first exercises

- repeated failed SSH attempts
- suspicious encoded PowerShell execution
- suspicious service creation on Windows
- repeated authentication attempts against a privileged account

## Recommended learning outcome

A junior analyst should be comfortable with triage, evidence review, alert validation, and basis-level incident response without needing advanced offensive security knowledge.
