# Architecture

This lab simulates a basic SOC environment for log collection, detection, and analysis.

## Components

- **Splunk Enterprise (Docker)** running on Ubuntu 22.04 LTS  
  - Configured as indexer and search head  
  - Windows logs ingested via Splunk Universal Forwarder  

- **Windows 11 VM (Log Source)**  
  - Generates security events (e.g., Event ID 4625, 4688)  
  - Used to simulate user activity and attack scenarios  

- **Kali Linux (Attack Simulation)**  
  - Used to generate suspicious activity and test detections  