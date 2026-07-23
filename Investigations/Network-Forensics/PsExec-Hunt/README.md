# PsExec Hunt

---

# Overview

This investigation analyzes a network packet capture (PCAP) containing evidence of an attacker performing lateral movement using Microsoft's PsExec utility.

The objective was to reconstruct the attack timeline, identify compromised systems and user accounts, determine how PsExec was deployed, and understand how the attacker moved across the network.

---

# Scenario

An Intrusion Detection System (IDS) generated an alert indicating suspicious SMB traffic consistent with PsExec activity.

As a SOC Analyst, the objective is to analyze the provided PCAP file using Wireshark to determine:

- Initial compromised machine
- Pivoted hosts
- Authenticated user
- PsExec service executable
- Administrative shares
- Communication channels
- Evidence of lateral movement

---

# Objectives

- Investigate SMB traffic
- Analyze NTLM authentication
- Identify compromised hosts
- Identify compromised credentials
- Recover transferred files
- Detect PsExec deployment
- Reconstruct attacker timeline

---

# Environment

Category:

- Network Forensics

Tool:

- Wireshark

Protocols:

- SMB
- SMB2
- NTLMSSP

Operating System:

- Windows Active Directory Environment

---

# Skills Practiced

- Network Forensics
- SMB Investigation
- NTLM Authentication Analysis
- Windows Administrative Shares
- Lateral Movement Investigation
- Timeline Reconstruction
- IOC Identification
- Wireshark Packet Analysis

---

# Investigation Methodology

The investigation followed a structured DFIR workflow.

1. Review network conversations
2. Identify suspicious SMB negotiations
3. Identify the initial compromised machine
4. Identify the first pivot host
5. Extract NTLM authentication details
6. Recover transferred SMB objects
7. Identify PsExec deployment
8. Identify administrative shares
9. Confirm communication channel
10. Identify second pivot host
11. Reconstruct the attack timeline

---

# Evidence Collection

Evidence was collected from:

- SMB Negotiation
- SMB Session Setup
- NTLM Challenge
- NTLM Authenticate
- Tree Connect Requests
- SMB Exported Objects

Wireshark features used:

- Statistics → Conversations
- Export Objects → SMB
- Packet Details
- Display Filters

---

# Analysis

## Step 1 — Initial Compromise

SMB negotiation traffic was analyzed to determine the first source system initiating SMB connections.

Display Filter

smb.cmd == 0x72

or

smb2.cmd == 0x00

Result:

Initial compromised machine identified.

---

## Step 2 — First Pivot

NTLM Challenge packets were inspected.

Display Filter

ntlmssp.challenge.target_name

The Target Name field identified the first system targeted during lateral movement.

---

## Step 3 — Authentication

NTLM Authenticate packets revealed the account used during authentication.

Display Filter

ntlmssp.auth.username

---

## Step 4 — PsExec Deployment

SMB Export Objects was used to recover transferred files.

Recovered executable confirmed PsExec service deployment.

---

## Step 5 — Administrative Share

Tree Connect packets identified the Windows administrative share used to copy the executable.

Display Filter

smb2.tree

---

## Step 6 — Communication Share

Additional Tree Connect packets identified the IPC communication channel established after deployment.

---

## Step 7 — Second Pivot

Subsequent NTLM Challenge packets identified the second host targeted by the attacker.

---

# Findings

The attacker successfully performed lateral movement using PsExec.

The investigation identified:

- Initial compromised workstation
- Multiple pivoted hosts
- Authenticated user account
- PsExec service executable
- Administrative share
- IPC communication share
- Second pivot target

The complete attack chain was reconstructed using only network evidence.

---

# Indicators of Compromise

See IOC/indicators.md

---

# MITRE ATT&CK Mapping

See MITRE/mitre-mapping.md

---

# Detection Opportunities

See Detection/

---

# Lessons Learned

See Notes/lessons-learned.md

---

# References

CyberDefenders

MITRE ATT&CK

Microsoft SMB Documentation

Microsoft PsExec Documentation

Wireshark Documentation
