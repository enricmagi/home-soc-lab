Day 3 — Windows Log Ingestion into Splunk SIEM
Objective

Configure a real log ingestion pipeline from a Windows endpoint to a Splunk SIEM in a home SOC lab, enabling visibility of Windows Security Events for detection and incident analysis.

Environment
Infrastructure

SIEM: Splunk Enterprise (Docker on Ubuntu Server)

Endpoint: Windows VM with Splunk Universal Forwarder

Network: Isolated Host-Only SOC network + NAT for SIEM internet access

Key Components

Splunk receiving port: 9997/TCP

Forwarder service: Running as Local System

Log source: WinEventLog Security

Implementation Steps
1. Network validation

Verified connectivity between Windows and Splunk.

Confirmed TCP reachability using:

telnet <splunk_ip> 9997


Result: Successful connection → network path operational.

2. Forwarder installation

Installed Splunk Universal Forwarder (Windows x64) with:

Deployment Server: Skipped

Receiving Indexer: <splunk_ip>:9997

Service Account: Local System

Default installation path preserved.

3. Input configuration (root cause resolution)

Initial ingestion failure traced to:

inputs.conf saved incorrectly as .txt
→ forwarder loaded no Windows event inputs
→ zero data indexed


Corrective action:

Created valid configuration:

C:\Program Files\SplunkUniversalForwarder\etc\apps\search\local\inputs.conf


Content:

[WinEventLog://Security]
disabled = 0
index = windows
renderXml = true


Restarted forwarder service:

Restart-Service SplunkForwarder

4. Data ingestion verification

Performed controlled event generation:

Failed logon attempts → EventCode 4625


Validated in Splunk:

index=windows EventCode=4625


Result:
Windows Security Events successfully indexed and searchable.

Troubleshooting Performed
Issue 1 — No events in Splunk

Cause:
Misnamed inputs.conf.txt prevented input loading.

Resolution:
Correct file extension + service restart.

Issue 2 — Delayed event visibility

Cause:

Forwarder queue initialization

Splunk indexing latency in resource-constrained VM

Resolution:
Waited for pipeline stabilization and generated fresh events.

Outcome
Technical Achievement

Successfully built a functional SOC ingestion pipeline:

Windows Security Logs → Splunk Universal Forwarder → Splunk Indexer → Searchable Events

SOC-Relevant Capabilities Demonstrated

SIEM log onboarding

Forwarder troubleshooting

Network connectivity validation

Windows Security Event generation & verification

Root-cause analysis of ingestion failure

Security Visibility Gained

Confirmed ingestion of key authentication events:

4624 — Successful logon

4625 — Failed logon

4634 — Logoff

These events form the foundation for:

Brute-force detection
Credential abuse monitoring
SOC L1 triage workflows

Conclusion

Day 3 marked the transition from infrastructure setup to operational SOC capability by enabling:

Real-time ingestion and analysis of Windows Security telemetry in Splunk.

This establishes the baseline required for:

Attack simulation

Detection engineering

Incident investigation

to be performed in subsequent lab stages.