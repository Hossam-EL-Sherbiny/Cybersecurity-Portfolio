# JetBrains Investigation
## Network Forensics | Web Server Compromise Investigation


## Overview

This investigation analyzes a simulated compromise of a JetBrains TeamCity server using network traffic captured in a PCAP file.
The objective was to reconstruct the attack timeline, identify the initial point of compromise, analyze the attacker's behavior, determine the uploaded malicious files, and collect evidence that could support incident response activities.
The investigation was performed primarily using Wireshark by analyzing HTTP traffic, POST requests, TCP streams, and network conversations.


## Scenario

A web server running JetBrains TeamCity showed signs of unauthorized activity.
Network traffic was provided to determine how the attacker gained access, what actions were performed after the compromise, and whether malicious files were uploaded to the server.
The investigation focuses on reconstructing the attack from the available network evidence.


## Objectives

- Identify the initial point of compromise.
- Determine the attacker's IP address.
- Identify the vulnerable web endpoint.
- Analyze malicious HTTP POST requests.
- Identify uploaded webshells.
- Determine attacker activity after exploitation.
- Collect Indicators of Compromise (IOCs).
- Reconstruct the attack timeline.


## Environment

| Item | Value |
|------|------|
| Platform | CyberDefenders |
| Category | Network Forensics |
| Primary Tool | Wireshark |
| Supporting Tools | NetworkMiner |
| Evidence Type | PCAP |
| Target | JetBrains TeamCity Server |


## Skills Practiced

- Network Traffic Analysis
- HTTP Protocol Analysis
- Packet Inspection
- TCP Stream Reconstruction
- Web Server Investigation
- IOC Extraction
- Timeline Reconstruction
- Webshell Detection

## Investigation Methodology

## The investigation followed a structured workflow:
1. Inspect overall network traffic.
2. Identify suspicious HTTP activity.
3. Focus on HTTP POST requests.
4. Analyze uploaded content.
5. Follow TCP Streams.
6. Identify attacker IP.
7. Identify uploaded webshells.
8. Reconstruct attacker actions.
9. Extract Indicators of Compromise.
10. Map attacker behavior to MITRE ATT&CK.


## Evidence Collection

## The following evidence was collected during the investigation:
- HTTP POST requests
- Uploaded files
- HTTP responses
- TCP conversations
- Source and destination IP addresses
- Web server version
- Request URIs
- Uploaded webshell filename


## Analysis

The investigation began by reviewing HTTP traffic generated during the capture.
HTTP POST requests immediately attracted attention because POST is commonly used to upload files or submit administrative actions.
One POST request targeted the TeamCity plugin upload endpoint, suggesting that the attacker exploited administrative functionality to upload a malicious file.
Following the TCP stream confirmed the successful upload of a webshell.
Subsequent HTTP requests demonstrated that the uploaded file was actively used to execute commands against the compromised server.
Further analysis identified the attacker IP address, reconstructed the sequence of events, and confirmed successful command execution.


## Findings

## The investigation confirmed that:
- The attacker successfully compromised the TeamCity server.
- A vulnerable administrative endpoint was abused.
- A malicious webshell was uploaded.
- The webshell was later used for command execution.
- Multiple HTTP requests confirmed attacker interaction with the compromised server.
- Network evidence allowed the complete reconstruction of the attack sequence.


## Indicators of Compromise

See:
IOC/ioc.md


## MITRE ATT&CK Mapping

See:
MITRE/mitre.md


## Detection Opportunities

## Potential detections include:
- Monitor unusual HTTP POST requests.
- Detect plugin uploads.
- Alert on unexpected JSP files.
- Detect suspicious command execution via HTTP.
- Monitor webshell creation.


## Lessons Learned

- HTTP POST requests often reveal attacker uploads.
- Following TCP Streams provides critical visibility into attacker activity.
- Network conversations help prioritize suspicious hosts.
- Webshell uploads can often be identified without endpoint logs.
- Small artifacts within network captures can reconstruct an entire attack.


