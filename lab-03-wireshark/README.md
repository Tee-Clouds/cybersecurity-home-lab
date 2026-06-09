# Lab 03 — Network Traffic Capture & Analysis

**Tool:** Wireshark 4.x  
**Capture Interface:** eth0 — Kali Linux (192.168.56.102)  
**Network Scope:** 192.168.56.0/24  
**Full Report:** [wireshark-capture-report.docx](./wireshark-capture-report.docx)

---

## Objective
Capture and analyze live network traffic between lab VMs to identify cleartext credentials, protocol weaknesses, and attack traffic patterns using Wireshark.

---

## Capture Sessions

### Session 1 — FTP Cleartext Credentials
```
Filter: ftp || ftp-data
```
- USER and PASS commands captured in plaintext
- Full FTP session visible with no encryption

### Session 2 — Telnet Session Capture
```bash
telnet 192.168.56.101
```
- Every keystroke visible in packet payload
- Username, password, and all commands in cleartext

### Session 3 — Nmap Scan Traffic
```
Filter: tcp.flags.syn == 1 && tcp.flags.ack == 0
```
- Rapid SYN packets across all ports clearly visible
- Pattern easily detectable by any IDS/IPS

### Session 4 — SMB Authentication
```
Filter: smb || nbns || dcerpc
```
- SMBv1 in use on Metasploitable
- NTLM challenge-response captured — hash extractable offline

---

## Findings Summary

| Protocol | Severity | Finding |
|---|---|---|
| FTP | 🔴 Critical | Cleartext credentials intercepted |
| Telnet | 🔴 Critical | Full session plaintext — keystrokes visible |
| SMBv1 | 🟠 High | Legacy protocol — NTLM hash capture possible |
| Nmap SYN Scan | ℹ️ Info | Scan pattern clearly detectable via IDS |
| DNS | 🟡 Low | Unencrypted queries reveal activity |

---

## Recommendations
- Replace FTP with SFTP or FTPS
- Disable Telnet — use SSH only
- Disable SMBv1 via GPO
- Implement IDS/IPS for scan detection
- Deploy DNS over HTTPS (DoH)

---

## Skills Demonstrated
`Wireshark` `Packet Analysis` `Protocol Analysis` `Network Security Monitoring` `FTP` `SMB` `NTLM`
