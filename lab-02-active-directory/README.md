# Lab 02 — Active Directory Setup & Enumeration

**Tool:** Active Directory DS, PowerShell, enum4linux, ldapsearch  
**Domain:** lab.local  
**Domain Controller:** WIN-DC01 (192.168.56.100)  
**Attacker:** Kali Linux (192.168.56.102)  
**Full Report:** [ad-enumeration-report.docx](./ad-enumeration-report.docx)

---

## Objective
Configure a Windows Server 2022 Active Directory domain (lab.local) and perform AD enumeration from a Kali Linux attacker machine using both SMB and LDAP techniques.

---

## AD Environment Configured

| Setting | Value |
|---|---|
| Domain | lab.local |
| Forest Functional Level | Windows Server 2016 |
| DNS Server | 192.168.56.100 |

### Organizational Units Created
- `OU=Users,DC=lab,DC=local`
- `OU=Computers,DC=lab,DC=local`
- `OU=Groups,DC=lab,DC=local`

### Test Accounts Created

| Username | Role | Group |
|---|---|---|
| Administrator | Domain Admin | Domain Admins |
| jdoe | Standard User | Domain Users |
| svcaccount | Service Account | Domain Users |

---

## Enumeration Commands

```bash
# SMB enumeration
enum4linux -a 192.168.56.100

# LDAP enumeration
ldapsearch -x -H ldap://192.168.56.100 -b 'DC=lab,DC=local'
```

---

## Key Findings

| Finding | Severity |
|---|---|
| Anonymous LDAP bind allowed — full domain queryable without credentials | 🔴 Critical |
| Null SMB session permitted — user list and password policy exposed | 🔴 Critical |
| Weak password policy — minimum 7 characters, no lockout | 🟠 High |
| Service account (svcaccount) identified — Kerberoasting candidate | 🟠 High |

---

## Recommendations
- Disable anonymous LDAP binds
- Restrict null SMB sessions via GPO
- Enforce 12+ character passwords with account lockout
- Audit service account SPNs

---

## Skills Demonstrated
`Active Directory` `Windows Server 2022` `AD DS` `enum4linux` `ldapsearch` `SMB Enumeration` `GPO`
