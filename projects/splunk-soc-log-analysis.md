# Splunk SOC Log Analysis Lab

## Objective

This lab demonstrates basic Security Operations Center (SOC) monitoring
and log analysis using Splunk. The goal is to ingest authentication
logs, investigate suspicious login activity, identify potential
brute-force behavior, and create basic visualizations and alerts.

## Tools

-   Splunk Enterprise / Splunk Free
-   Windows
-   Authentication log dataset
-   SPL (Search Processing Language)

## Lab Scenario

A user account is experiencing multiple failed login attempts. Acting as
a SOC analyst, the objective is to analyze authentication logs and
determine whether the activity may represent a brute-force attempt.

## Tasks Performed

-   Imported authentication logs into Splunk
-   Searched and filtered security events
-   Identified repeated failed login attempts
-   Identified source IP addresses generating failures
-   Compared failed and successful authentication events
-   Investigated successful logins following multiple failures
-   Created a basic security dashboard
-   Configured a basic alert for excessive failed logins

## SPL Queries

### 1. View Authentication Events

``` spl
index=main
| table _time user src_ip action
```

### 2. Failed Login Attempts

``` spl
index=main action="failure"
| table _time user src_ip
```

### 3. Count Failed Logins by Source IP

``` spl
index=main action="failure"
| stats count by src_ip
| sort - count
```

### 4. Failed Logins by User

``` spl
index=main action="failure"
| stats count by user
| sort - count
```

### 5. Detect IPs with Multiple Failed Attempts

``` spl
index=main action="failure"
| stats count by src_ip
| where count >= 5
| sort - count
```

### 6. Review Successful Logins

``` spl
index=main action="success"
| table _time user src_ip
```

## Investigation

The analysis focuses on identifying source IP addresses responsible for
multiple failed authentication attempts.

Repeated authentication failures from the same source may indicate
password guessing or brute-force activity. Successful authentication
events should also be reviewed to determine whether a successful login
occurred after repeated failures.

During triage, the analyst should consider:

-   Number of failed attempts
-   Source IP address
-   Targeted user account
-   Timing and frequency of the attempts
-   Whether a successful login followed the failures

## Dashboard

Create a simple Splunk dashboard containing:

1.  Failed login attempts over time
2.  Top source IP addresses by failed logins
3.  Users with the most failed authentication attempts
4.  Successful vs. failed authentication events

## Basic Alert

Configure an alert based on the following search:

``` spl
index=main action="failure"
| stats count by src_ip
| where count >= 5
```

The alert identifies source IP addresses generating five or more failed
authentication attempts within the selected search window.

## SOC Investigation Workflow

1.  **Detect** - Identify unusual authentication activity.
2.  **Triage** - Determine the affected account, source IP, and number
    of attempts.
3.  **Investigate** - Review related failed and successful
    authentication events.
4.  **Document** - Record the searches performed and relevant findings.
5.  **Escalate** - Escalate suspicious activity when additional
    investigation or response is required.
6.  **Monitor** - Create a dashboard or alert to identify similar
    activity.

## Skills Practiced

-   Splunk
-   SPL
-   SIEM fundamentals
-   Log analysis
-   Security monitoring
-   Authentication analysis
-   Basic incident triage
-   Brute-force detection
-   Dashboard creation
-   Alert configuration
-   SOC investigation workflow

## Suggested Evidence for This Repository

Add screenshots after completing the lab:

-   `screenshots/01-data-ingestion.png`
-   `screenshots/02-failed-logins.png`
-   `screenshots/03-top-source-ips.png`
-   `screenshots/04-dashboard.png`
-   `screenshots/05-alert.png`

Example:

``` markdown
![Failed Login Investigation](screenshots/02-failed-logins.png)
```

## Conclusion

This lab provides hands-on practice using Splunk as a SIEM platform to
search, analyze, and correlate authentication events. It demonstrates a
basic SOC workflow: detecting suspicious activity, triaging events,
investigating related logs, documenting findings, and configuring
monitoring for similar activity.

## Disclaimer

This project is a learning lab performed in a controlled environment
using simulated or authorized data. It is intended to demonstrate
foundational Splunk and SOC analysis skills.
