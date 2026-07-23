# Lessons Learned

- SMB negotiation can identify the attacker's initial activity.
- NTLM Challenge messages reveal the destination host.
- NTLM Authenticate messages reveal the username used during authentication.
- Administrative shares (ADMIN$) are commonly used by PsExec to deploy service binaries.
- IPC$ is used as the communication channel after service deployment.
- Exporting SMB objects from Wireshark allows recovery of transferred executables.
- Multiple pieces of evidence must be correlated to reconstruct the full attack timeline.
