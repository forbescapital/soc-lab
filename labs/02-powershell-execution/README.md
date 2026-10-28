# Suspicious PowerShell Lab

## Scenario

Investigate a Windows endpoint where a PowerShell process runs an encoded command.

## Objective

Identify whether the PowerShell execution is malicious or a legitimate admin activity.

## Questions to answer

- Who triggered the process?
- What user context was used?
- What command was executed?
- Was the script base64-encoded?
- Was the parent process suspicious?
- Did the command spawn further processes?

## Step-by-step procedure

1. Search Sysmon or Windows Event Logs for `powershell.exe` with `EncodedCommand`.
2. Review the parent process and user account.
3. Decode the PowerShell command if possible.
4. Inspect any child processes created by PowerShell.
5. Check whether the host later performed network or persistence activity.
6. Record the final assessment.

## Example findings

- `powershell.exe` launched by `cmd.exe`
- encoded command executed by a standard user
- no approved admin task associated with the command
- suspicious network connection followed shortly afterward

## Analyst note

PowerShell is commonly abused by attackers because it can execute scripts without dropping a file. Encoded commands can hide intent and should be investigated promptly.
