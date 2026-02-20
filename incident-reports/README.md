This will be the template for every single incident

Incident Report — [Incident title]

Example:

Brute Force Attempt — Multiple Failed Logons

1. Executive Summary

On [DATE] around [TIME UTC], suspicious activity was detected on host [HOSTNAME].

The activity involved [short description], indicating a potential [type of attack].

No evidence of successful compromise was observed.


2. Alert Details

Detection Name: [Detection name]

Log Source: [Windows Security Logs / Sysmon / etc]

Event ID(s): [IDs]

Host: [HOSTNAME]

Source IP: [IP or N/A]

Severity: Low / Medium / High


3. Timeline of Events
Time (UTC)	Event	Details
[TIME]	[Event]	[Details]


4. Investigation & Analysis

Analysis revealed the following:

Observed activity:

[Details]

Identified pattern:

[Pattern]

Reason for suspicion:

[Why it is suspicious]

Additional observations:

[Frequency / volume]

[Time range of activity]

[Technical context]

Conclusion:

[Explain why this activity is considered an incident or anomaly]


5. Impact Assessment

Successful compromise: Yes / No

Lateral movement: Yes / No

Persistence: Yes / No

Impact Summary:

[Describe the actual impact]


6. Actions Taken

Actions performed or recommended:

Analysis conducted:

Response actions required:


7. Recommendations

[Specific recommendation]

[Another concrete measure]


8. Detection Logic (Splunk SPL)
[QUERY]

Explanation:
[2–3 sentences explaining detection logic]


9. Screenshots

Detection query results

Relevant logs (Splunk / Event Viewer)

Supporting evidence