# splunk-soc-bruteforce-detection

Overview

This project demonstrates basic Security Operations Center (SOC) monitoring using Splunk. Windows Event Logs were ingested into Splunk to detect and analyze failed login attempts.

Tools Used
Splunk Enterprise
Windows Event Viewer
Windows Security Logs

Data Source
Windows Event Logs (Security)
EventCode 4625 (Failed logins)
EventCode 4624 (Successful logins)

Detection Logic

Failed Login Detection
index=wineventlog EventCode=4625
| stats count by src, Account_Name

Brute Force Detection Rule
index=wineventlog EventCode=4625
| bin _time span=5m
| stats count by _time, src, Account_Name
| where count >= 3

What I Learned
How to ingest Windows logs into Splunk
How authentication logs are structured
How to detect brute force patterns using SPL
Basic SOC investigation workflow
