# 🔬 Cybersecurity Home Lab

A hands-on home lab environment built to develop real-world offensive and defensive security skills.

## 🖥️ Lab Environment
- **Hypervisor:** VirtualBox
- **Network:** Isolated Host-Only (192.168.56.0/24)
- **Domain:** lab.local

## 🖧 Virtual Machines
| VM | Role |
|---|---|
| Windows Server 2022 | Domain Controller (lab.local) |
| Kali Linux | Attacker Machine |
| Metasploitable 2 | Vulnerable Target |
| Ubuntu 22.04 | Linux Target |
| OWASP BWA | Web App Target |

## 📁 Labs
| Lab | Description |
|---|---|
| [Lab 01 - Nmap Scanning](./lab-01-nmap-scanning/) | Network discovery and port scanning |
| [Lab 02 - Active Directory](./lab-02-active-directory/) | AD setup, enumeration, and attacks |
| [Lab 03 - Wireshark](./lab-03-wireshark/) | Traffic capture and analysis |
| [Lab 04 - Metasploit](./lab-04-metasploit/) | Exploitation using CVE-2011-2523 |

## 🎯 Goals
- Develop hands-on pentesting skills
- Document findings in professional pentest reports
- Build toward a Cloud Security Engineer role
