# Junior SOC Analyst Lab

This repository is a beginner-focused Security Operations Center (SOC) lab built for junior analysts learning how to work with a real SOC stack using Wazuh + Elastic Stack (ELK).

## Lab purpose

The lab teaches the real-world analyst workflow:

- collect logs from endpoints and servers
- identify suspicious behavior
- triage alerts
- investigate the timeline of activity
- validate and tune detections
- document an investigation and escalate when needed

## Best stack for junior analysts

Wazuh + Elastic Stack is the best fit for beginners because it is:

- open source and cost-effective
- realistic for SOC operations
- easy to learn with a small lab environment
- rich in endpoint, authentication, and process telemetry
- suitable for training detections, hunting, and IR workflows

## Recommended environment

- 1 SIEM server running Wazuh + Elasticsearch + Kibana
- 1 Windows endpoint running Sysmon + Microsoft Defender
- 1 Linux server generating SSH, auth, and web logs
- 1 Kali or attacker VM for lab simulations

## Learning objectives

By the end of this lab, a junior analyst should be able to:

- understand common SOC data sources
- investigate failed logins and suspicious PowerShell execution
- review endpoint and authentication telemetry
- identify persistence and privilege escalation indicators
- triage alerts with context
- produce concise investigation notes and escalation summaries

## Repository structure

- `docs/` — environment architecture and setup guides
- `detections/` — Sigma rules and detection examples
- `labs/` — beginner exercises and investigations
- `playbooks/` — triage and response workflows
- `scripts/` — log generation and sample data helpers

## Suggested lab flow

1. Set up the SIEM environment
2. Deploy the Windows and Linux endpoints
3. Enable Sysmon and logging on endpoints
4. Investigate the first brute-force exercise
5. Review suspicious process activity
6. Tune rules and build a timeline
7. Escalate findings with a documented summary

## Recommended training path

- Week 1: Log review, alert triage, authentication events
- Week 2: PowerShell, process execution, and endpoint behaviors
- Week 3: Persistence, scheduled tasks, and privilege abuse
- Week 4: Threat hunting and incident response playbooks

## Example use cases

- SSH brute force attempts
- PowerShell encoding for malicious execution
- Account lockouts and password spray activity
- Suspicious scheduled task creation
- Privilege escalation indicator review

## Quick start

Read through the setup and architecture docs before deploying the lab.

1. Review `docs/lab-architecture.md`
2. Follow the steps in `docs/environment-setup.md`
3. Deploy the endpoint clients
4. Run the first lab in `labs/01-bruteforce-login/`
5. Investigate the process execution lab in `labs/02-powershell-execution/`

## Tools covered

- Wazuh
- Elasticsearch
- Kibana
- Sysmon
- Windows Event Logs
- Linux authentication logs
- Sigma
- Atomic Red Team (optional)

## License

MIT
