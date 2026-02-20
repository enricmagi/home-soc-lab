Incident Report — [Incident title]

Example:

Brute Force Attempt — Multiple Failed Logons

1. Executive Summary

On 02/20/2026 around 11:55 AM UTC (12:55 local time, UTC+1), suspicious activity was detected on host DESKTOP-4RB9T57.

The activity involved several failed login attempt with fake credentials, indicating a potential Brute Force assault.

No evidence of successful compromise or login was observed.


2. Alert Details

Detection Name: Brute Force Detection

Log Source: Windows Security Logs

Event ID(s): 4625

Host: DESKTOP-4RB9T57

Source IP: 127.0.0.1

Severity: Medium


3. Timeline of Events
Time (UTC)	   Event	           Details
11:55:00       Failed Logon        User: FakeUser1
11:55:XX       Multiple failures   ~20 failed attempts across multiple usernames


4. Investigation & Analysis

Analysis revealed the following:

Observed activity:

Multiple Windows Security Event ID 4625 entries were detected in Splunk within a short time window

Identified pattern:

Repeated failed authentication attempts targeting multiple usernames (FakeUser1–FakeUser20, showing a i++ pattern command).

Reason for suspicion:

The volume and frequency of failed logon attempts are inconsistent with normal user behavior and suggest automated activity.

Additional observations:

Approximately 20 failed attempts occurred within a few minutes.

Activity was limited to a single host.

Authentication attempts were performed using NTLM with Logon Type 3 (network logon).

Conclusion:

The observed behavior is consistent with a brute force attack attempt, where multiple authentication attempts are made in a short period of time against different user accounts.


5. Impact Assessment

Successful compromise: No

Lateral movement: No

Persistence: No

Impact Summary:

No successful authentication was observed. The activity represents a failed brute force attempt with no impact on system integrity.


6. Actions Taken

Actions performed or recommended: Activity was analyzed using Splunk SIEM

Analysis conducted: Review of Windows Security logs (Event ID 4625) and correlation of repeated failed attempts.

Response actions required: o immediate action required due to lack of successful compromise.


7. Recommendations

· Implement account lockout policies to prevent repeated authentication attempts.

· Enable monitoring and alerting for multiple failed logon attempts.


8. Detection Logic (Splunk SPL)

index=* EventCode=4625
| bucket _time span=5m
| stats count by _time, host
| where count >= 5
| sort -count

Explanation:

This query identifies multiple failed logon attempts within a defined time window, which may indicate brute force activity.


9. Screenshots

Screenshots supporting this analysis are available in the "screenshots" directory; they include:

Detection query results

Relevant Windows Security logs

Supporting evidence from Splunk