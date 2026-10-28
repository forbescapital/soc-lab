# Brute Force Login Lab

## Scenario

Investigate repeated failed SSH authentication attempts against a Linux host.

## Objective

Determine whether the activity is a brute force or password spray attempt and decide whether it should be escalated.

## Questions to answer

- Which host was targeted?
- Which username was being attacked?
- From which IP did the activity originate?
- Did any login eventually succeed?
- Did any suspicious follow-on activity occur on the endpoint?

## Step-by-step procedure

1. Search the SSH or auth logs for repeated failed login events.
2. Group by source IP and username.
3. Identify whether the same IP is performing multiple attempts.
4. Check whether the user account is privileged.
5. Review whether a successful login occurred after the burst.
6. Capture the timeline and write an analyst summary.

## Example findings

- 22 failed logins against `admin` from `203.0.113.44`
- all attempts came from a single external IP
- there was no successful login
- however, the event is still suspicious and should be reviewed for blocking or IP containment

## Analyst note

Repeated failed authentication attempts are often part of a brute-force or password-spraying campaign. Even when no login succeeds, the source should be reviewed and the activity may be worth documenting as an attempted intrusion.
