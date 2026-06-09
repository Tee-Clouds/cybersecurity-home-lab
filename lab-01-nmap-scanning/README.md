# Lab 01 — Network Discovery & Port Scanning

**Tool:** Nmap 7.94  
**Attacker:** Kali Linux (192.168.56.102)  
**Network Scope:** 192.168.56.0/24  
**Full Report:** [nmap-scan-report.docx](./nmap-scan-report.docx)

---

## Objective
Perform host discovery and service enumeration across the isolated lab network to simulate the reconnaissance phase of a penetration test.

---

## Commands Used

```bash
# Host discovery
nmap -sn 192.168.56.0/24

# Full port scan with service and OS detection
nmap -sV -sC -O -p- 192.168.56.0/24 -oN nmap_full.txt
```

---

## Hosts Discovered

| IP Address | Hostname | OS | Role |
|---|---|---|---|
| 192.168.56.100 | WIN-DC01 | Windows Server 2022 | Domain Controller |
| 192.168.56.101 | metasploitable | Linux 2.6.x | Vulnerable Target |
| 192.168.56.102 | kali | Kali Linux | Attacker Machine |
| 192.168.56.103 | ubuntu-target | Ubuntu 22.04 | Linux Target |
| 192.168.56.104 | owasp-bwa | Linux | Web App Target |

---

## Notable Open Ports — Metasploitable (192.168.56.101)

| Port | Service | Notes |
|---|---|---|
| 21/tcp | vsftpd 2.3.4 | ⚠️ Backdoor — CVE-2011-2523 |
| 22/tcp | OpenSSH 4.7p1 | Outdated version |
| 23/tcp | Telnet | Cleartext — no encryption |
| 80/tcp | Apache 2.2.8 | OWASP web apps |
| 3306/tcp | MySQL 5.0.51a | No root password |
| 5900/tcp | VNC | No authentication |
| 1524/tcp | Bindshell | Open root shell |

---

## Key Findings

- **5 live hosts** discovered on the subnet
- **Multiple critical services** running on Metasploitable with no authentication
- **CVE-2011-2523** (vsftpd backdoor) identified — exploited in Lab 04
- Scan pattern is detectable by IDS — SYN packets across all 65535 ports

---

## Skills Demonstrated
`Nmap` `Network Reconnaissance` `Port Scanning` `Service Enumeration` `OS Fingerprinting`
