Home SOC Lab – Days 1–2 Setup & Troubleshooting
Overview
During the first two days, a functional SOC laboratory with Splunk as SIEM was built using local virtualization.
The objective was to reach a working Splunk web interface ready to ingest logs from simulated endpoints.

Day 1 – Infrastructure Preparation
Goals
Prepare virtualization environment
Create isolated SOC lab network
Deploy three virtual machines:
Splunk server (Ubuntu)
Windows endpoint (victim)
Kali Linux attacker
Actions Performed
1. Hypervisor selection
VirtualBox initially presented network driver and host‑only adapter errors.
Decision taken:
Switch to VMware Workstation for:
Better Windows 11 compatibility
Stable virtual networking
Faster troubleshooting path
2. Virtual machine creation
Three VMs were created:
VM
Purpose
Key Resources
SOC‑SPLUNK
SIEM server
4 GB RAM, 40 GB disk
SOC‑WIN11
Log source
3 GB RAM
SOC‑KALI
Attacker simulation
2 GB RAM

All machines configured with:
Host‑only network for internal SOC traffic
Later adjusted to:
NAT + Host‑Only dual interface on Splunk
NAT → Internet access
Host‑Only → SOC internal visibility
Key Troubleshooting (Day 1)
VirtualBox network driver failure
Error:
VERR_INTNET_FLT_IF_NOT_FOUND

Root cause: Windows host‑only driver not loaded.
Resolution:
Abandoned VirtualBox
Migrated to VMware
Lesson:
Engineering time should prioritize lab progress, not tooling issues.

Day 2 – Ubuntu & Splunk Deployment
Goals
Install Ubuntu Server
Deploy Splunk Enterprise
Achieve working SIEM web access
Ubuntu Installation
Key configuration:
DHCP networking
OpenSSH installed
Minimal services
LVM default disk layout
Issue: No Internet during install
Cause: Host‑only network only.
Fix:
Added NAT adapter to Splunk VM

Splunk Installation Attempts
Problem Chain Observed
1. Corrupted .deb download
Error:
not a Debian format archive

Cause: invalid/partial download.
Fix: re‑download official package.

2. Broken first initialization
Symptoms:
Web UI accessible
No admin user exists
CLI user creation failed
Reason:
Splunk initial bootstrap entered inconsistent state.
Engineering decision:
Stop wasting time on broken install → switch deployment method.

Pivot to Docker‑based Splunk
Rationale
Faster clean deployment
Deterministic admin creation
Common in modern infrastructure
Docker Setup Steps
Installed Docker Engine
Pulled official Splunk image
Launched container with:
License acceptance
Admin password preset
Port 8000 exposed

Major Troubleshooting (Day 2)
Disk space exhaustion
Error:
no space left on device

Finding:
VM disk = 40 GB
Root filesystem = 19 GB LVM
Resolution:
Expanded virtual disk
Resized LVM + filesystem
Real‑world relevance:
Classic Linux server storage troubleshooting scenario.

Splunk General Terms not accepted
Error: container refused to start.
Fix:
Added environment variable:
SPLUNK_GENERAL_TERMS="--accept-sgt-current-at-splunk-com"


Final State After Day 2
Working Components
Ubuntu SIEM host running
Docker operational
Splunk container deployed
Web UI accessible on:
http://<splunk-ip>:8000

Skills Demonstrated
Infrastructure
Hypervisor migration decision‑making
Virtual networking design (NAT vs Host‑Only)
Linux storage expansion with LVM
SIEM Deployment
Package troubleshooting
Service initialization debugging
Containerized Splunk deployment
SOC‑Relevant Knowledge
Separation of lab networks
Remote administration via SSH
Deterministic environment setup

Lessons Learned
Time management is critical in engineering labs.
Pivot early when installs become inconsistent.
Containerization reduces troubleshooting surface.
Faster path to functional SIEM.
Linux storage layouts matter.
Disk size ≠ usable filesystem.
Reaching a working SIEM is a major milestone.
Many beginners never achieve this stage.

Next Step (Day 3 Preview)
Objective:
Send Windows Security Event Logs → Splunk and begin:
Log analysis
Detection logic
SOC L1 triage simulation
This marks the transition from:
Infrastructure work → Real SOC operations


