# Detections

This section contains Splunk detection logic used across different incidents.

## Current detections

### Brute Force Detection (Windows Event ID 4625)

Detects multiple failed logon attempts within a short time window.

[spl]
index=* EventCode=4625
| bucket _time span=5m
| stats count by _time, host
| where count >= 5
| sort -count