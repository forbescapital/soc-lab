# Junior SOC Analyst Lab

A beginner-friendly Security Operations Center (SOC) lab built around Wazuh + Elastic Stack (OpenSearch/ELK alternatives are also possible), designed to teach junior analysts the core skills of log analysis, alert triage, and incident response.

## Why this stack?

Wazuh + Elastic Stack is the best starting point for junior analysts because it combines:

- Endpoint monitoring
- Log collection
- Alerting and rules
- Search and investigation workflows
- Realistic SOC tooling without enterprise licensing overhead

This lab emphasizes practical analyst skills over pure tooling complexity.

## Lab goals

By the end of the lab, a junior SOC analyst should be able to:

- Collect logs from Windows and Linux endpoints
- Investigate failed login attempts and suspicious user activity
- Review endpoint events and process execution
- Create and tune detection rules
- Triage alerts and document findings
- Practice basic incident response steps

## Recommended lab topology

- 1 Linux VM: Wazuh Manager + Elastic Stack
- 1 Windows VM: endpoint telemetry with Sysmon + Defender
- 1 Linux server: SSH, web logs, and sudo activity
- 1 Kali VM: attack simulation

## Core learning scenarios

1. Failed login brute force
2. Unusual PowerShell execution
3. New scheduled task or service creation
4. Lateral movement indicators
5. Privilege escalation attempts
6. Suspicious file execution from user-writable paths

## Repository layout

- `docs/` – architecture, setup, and learning plans
- `detections/` – Sigma rules and rule examples
- `playbooks/` – investigation and triage workflows
- `labs/` – hands-on exercises and scenarios
- `scripts/` – automation and helper tools
- `logs/` – sample data and parsers

## Quick start

1. Review `docs/lab-architecture.md`
2. Deploy the VM topology
3. Install Wazuh + Elastic Stack
4. Configure Windows/Linux agents
5. Start with the first lab in `labs/01-bruteforce-login/`
6. Investigate events and tune detections

## Suggested learning path

- Week 1: Log review and alert triage
- Week 2: Endpoint and authentication events
- Week 3: Persistence and privilege escalation
- Week 4: IOC hunting and incident response

## Recommended tools

- Wazuh
- Elastic Stack / OpenSearch
- Sysmon
- Atomic Red Team
- Sigma
- Windows Event Forwarding / WinRM

## Notes

This repository is intentionally starter-focused. It is designed to help beginners learn the SOC mindset: detect, validate, investigate, and document.

## License

MIT
