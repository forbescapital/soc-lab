# Junior SOC Analyst Learning Guide

This guide is intended for junior analysts learning how to work inside a SOC environment using SIEM tools, endpoint telemetry, and security detections.

## Mindset

A SOC analyst is not just a tool operator. Analysts must think in terms of:

- what happened
- when it happened
- who was involved
- what systems were affected
- whether the activity is malicious or benign
- what should be escalated

## Core skills covered

### 1. Alert triage

A junior analyst should learn how to determine:

- whether an alert is real
- if the alert is high, medium, or low severity
- which assets were involved
- whether the activity matches a known attack pattern

### 2. Log investigation

Students should understand how to review events such as:

- Windows Security logs
- Sysmon logs
- Linux auth logs
- web access logs
- PowerShell logs

### 3. Timeline analysis

Ask: what happened before, during, and after the suspicious event?

### 4. Detection tuning

Junior analysts should learn how to identify:

- noisy detections
- missing detections
- false positives
- where to add context or exclusions

### 5. Incident response basics

This includes:

- containment
- evidence collection
- escalation
- communication with stakeholders
- documentation

## Recommended training order

1. Collect logs and understand common fields
2. Review login failures and account lockouts
3. Investigate PowerShell execution
4. Review persistence methods
5. Build a timeline of suspicious activity
6. Write a concise incident summary

## Example investigation questions

- Who logged in and from where?
- Was the activity successful?
- Was there an account creation or password change?
- What process executed on the endpoint?
- Did the user run suspicious commands?
- Was the activity repeated or isolated?

## Sample analyst note

"At 14:22 UTC, the user `jdoe` experienced 18 failed logins from a remote host. Following the failure pattern, a PowerShell process launched on the endpoint and executed a suspicious encoded command. No malware was confirmed at the time of triage, but the activity is consistent with credential abuse and should be escalated for deeper host-based investigation."

## Best practice

Always document:

- timestamp
- affected host
- user involved
- source IP or remote host
- activity observed
- evidence referenced
- analyst conclusion

## Tools to practice with

- Wazuh
- Kibana / Discover
- Sysmon
- Windows Security Event Log
- Linux auth and system logs

## End goal

A junior SOC analyst should move from “alert consumer” to “evidence-based investigator.”
