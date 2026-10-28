# Brute Force Login Lab

## Scenario

Investigate a sequence of repeated login failures against an SSH service.

## Objective

Identify whether the activity is a brute force attempt and determine if it resulted in any successful unauthorized access.

## Questions to answer

- Which host was targeted?
- Which user account was attacked?
- What is the source IP?
- Did the activity escalate into a successful login?
- What would you do next?

## Suggested steps

1. Search SSH audit logs for repeated failed authentication events.
2. Review source IP addresses.
3. Check whether any accounts were locked or reset.
4. Confirm whether a successful SSH session occurred afterward.
5. Document findings and alert severity.

## Example evidence

- 25 failed logins in 5 minutes from the same IP
- no successful login
- repeated invalid usernames

## Analyst note

This pattern is highly consistent with password spraying or brute force activity. If no successful login occurred, the likely outcome is blocked access, but the source should still be investigated.
