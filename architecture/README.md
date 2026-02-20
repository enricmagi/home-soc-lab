# Architecture

This lab simulates a basic SOC environment for log collection, detection, and analysis.

## Components

- **VMware Workstation (Hypervisor running on the host machine)**
  - Used to run multiple virtual machines on a 6 core CPU and 16 GB RAM laptop  
  - Resource allocation:
    - Windows VM: 2 CPU cores  
    - Ubuntu VM: 2 CPU cores  
    - Kali Linux VM: 1 CPU core  

- **Splunk Enterprise (Docker) running on Ubuntu 22.04 LTS**  
  - Configured as indexer and search head  
  - Receives Windows logs via Splunk Universal Forwarder  

- **Windows 11 VM (Log Source)**  
  - Generates security events (e.g., Event ID 4625, 4688)  
  - Used to simulate user activity and attack scenarios  

- **Kali Linux (Attack Simulation)**  
  - Used to generate suspicious activity and validate detections  