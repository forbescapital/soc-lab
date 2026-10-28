# Incident Response and Analyst Workflow

This playbook covers the basic workflow a junior SOC analyst should follow while investigating alerts.

## Step 1: Validate the alert

Check:

- host name
- user account
- time of event
- source IP or remote host
- severity and detection rule

## Step 2: Gather context

Review:

- authentication history
- process creation records
- Windows service creation or scheduled task creation
- web server logs
- system and admin activity in the same time window

## Step 3: Build a timeline

Map events in order:

- before the alert
- at the time of the alert
- after the alert

## Step 4: Determine business impact

Ask:

- Is this user expected to do this activity?
- Was the activity targeted or broad?
- Was there a successful login or privilege escalation?
- Was the host compromised or just noisy?

## Step 5: Response actions

If malicious behavior is confirmed:

- isolate the endpoint if needed
- disable or reset affected accounts
- preserve logs and forensic artifacts
- escalate to the senior analyst or IR team

## Step 6: Documentation

Your final note should include:

- summary of the activity
- affected hosts and users
- timeline of events
- evidence referenced
- analyst assessment
- recommended follow-up actions

## Example summary

"At 14:22 UTC, repeated SSH authentication failures were observed against the `svc-admin` account from IP 203.0.113.44. Within the same time window, an endpoint showed suspicious PowerShell execution with an encoded command. The activity is consistent with credential abuse and possible execution of malicious code. The event was escalated for deeper investigation and host isolation review."
