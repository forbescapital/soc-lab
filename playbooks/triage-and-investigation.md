# Triage and Investigation Playbook

## Goal

Provide a simple triage workflow for junior SOC analysts handling suspicious alerts.

## Step 1: Validate the alert

Check:

- host name
- user account
- source IP
- timestamp
- detection rule used

## Step 2: Enrich the context

Gather:

- previous activity from same host
- login history for user
- process execution history
- network connections
- scheduled tasks or services

## Step 3: Build the timeline

Create a sequence of events:

- before alert
- at alert time
- after alert

## Step 4: Determine maliciousness

Ask whether the event matches:

- brute force
- malware execution
- persistence
- privilege escalation
- data theft or exfiltration

## Step 5: Containment and escalation

If malicious activity is confirmed:

- isolate asset
- disable account if necessary
- preserve logs and forensic evidence
- escalate to senior analyst or incident responder

## Step 6: Documentation

Write:

- summary of the alert
- impacted systems
- attacker indicators
- response actions taken
- final analyst assessment

## Example final summary

"Alert triggered for repeated failed SSH authentication attempts from IP 203.0.113.44 against the `svc-admin` account. Subsequent endpoint telemetry showed a PowerShell process executing an encoded command. The activity was escalated as suspicious credential abuse with possible command execution."
