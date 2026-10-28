# SOC Lab Exercises

This doc outlines the recommended beginner exercises for the SOC lab.

## Exercise 1: Failed SSH logins

Objective: identify password spraying or brute-force attempts.

Tasks:

- review failed login attempts from the same IP
- identify the target username
- determine if the source IP is internal or external
- check whether any successful login followed
- document the impact and next steps

## Exercise 2: Suspicious PowerShell execution

Objective: analyze suspicious command execution.

Tasks:

- locate PowerShell process creation events
- identify encoded or obfuscated command strings
- map the parent process to the user activity
- determine whether the command is suspicious or benign
- assess if persistence or command-and-control is likely

## Exercise 3: Suspicious service creation

Objective: detect persistence methods.

Tasks:

- review Windows Security logs for service creation
- confirm the service name and binary path
- identify the system account used
- correlate with the same host timeline
- decide whether to escalate

## Exercise 4: Privilege escalation review

Objective: recognize common escalation behavior.

Tasks:

- review UAC or token elevation events
- look for `whoami /groups`, `net localgroup administrators`, or suspicious scheduled tasks
- compare to normal administrator activity
- confirm if the host is under attack

## Exercise 5: Timeline building

Objective: reconstruct an incident.

Tasks:

- identify the first malicious event
- then identify the next suspicious step
- map all related user, process, and network events
- summarize the attack chain in plain language

## Deliverable

Each exercise should end with:

- alert summary
- evidence list
- timeline
- analyst conclusion
- recommended response action
