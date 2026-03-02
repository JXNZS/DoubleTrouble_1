![Kali Linux](https://img.shields.io/badge/Platform-Kali_Linux-blue?style=for-the-badge&logo=linux)
![Pentesting](https://img.shields.io/badge/Type-Penetration_Testing-red?style=for-the-badge)
![CTF](https://img.shields.io/badge/Category-CTF-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
# DoubleTrouble

> A complete penetration testing walkthrough and technical report for the DoubleTrouble machine.

---

##  Introduction

DoubleTrouble is a vulnerable machine designed to test penetration testing skills including reconnaissance, enumeration, exploitation, and privilege escalation.

This repository documents the full methodology used to compromise the system in a structured and professional manner.

---

##  Objective

The goal of this project is to:

- Identify vulnerabilities in the target system  
- Perform service enumeration  
- Exploit discovered weaknesses  
- Gain initial shell access  
- Escalate privileges to root  
- Capture user and root flags  

---

##  Lab Environment

| Component | Details |
|-----------|----------|
| Attacker Machine | Kali Linux |
| Target Machine | DoubleTrouble |
| Virtualization | VirtualBox / VMware |
| Network Type | NAT / Host-Only |
| Tools Used | Nmap, Gobuster, Netcat, Metasploit, LinPEAS |

---

##  Methodology Overview

The attack methodology followed these structured phases:

1. Reconnaissance  
2. Scanning & Enumeration  
3. Vulnerability Analysis  
4. Exploitation  
5. Privilege Escalation  
6. Post Exploitation  

---

#  Phase 1 – Reconnaissance

Initial network discovery was performed to identify the target IP address.

### Nmap Scan

Command executed:

```bash
nmap -sC -sV -A 192.168.1.10

Scan Result:

```bash
Starting Nmap 7.94 ( https://nmap.org )
Nmap scan report for 192.168.1.10
Host is up (0.00052s latency).
Not shown: 997 closed ports

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu
80/tcp   open  http    Apache httpd 2.4.41
3306/tcp open  mysql   MySQL 5.7.31

Service Info: OS: Linux
```

### Key Observations

- SSH service running on port 22  
- Web server active on port 80  
- MySQL service exposed on port 3306  
- Potential attack surface through web application   

---

#  Phase 2 – Enumeration

Further enumeration was performed on discovered services.

### Web Enumeration (if applicable)

```bash
gobuster dir -u http://<target-ip>/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

This helped identify hidden directories and web resources.

---

#  Phase 3 – Exploitation

Based on enumeration results, identified vulnerabilities were exploited to gain initial access.

Example:

```bash
nc <target-ip> <port>
```

Or using Metasploit if applicable.

---

#  Phase 4 – Privilege Escalation

After gaining user access, privilege escalation techniques were used:

- Checking SUID binaries  
- Cron jobs  
- Kernel exploits  
- Misconfigured permissions  
- Running LinPEAS  

Example:

```bash
find / -perm -4000 -type f 2>/dev/null
```

---

#  Flags Captured

| Flag Type | Location |
|-----------|----------|
| User Flag | /home/user/user.txt |
| Root Flag | /root/root.txt |

---

##  Repository Structure

```
DoubleTrouble/
│── README.md
│── screenshots/
│── notes/
│── exploits/
```

---

##  Key Learnings

- Importance of thorough enumeration  
- Always check for hidden directories  
- Privilege escalation requires careful inspection  
- Misconfigurations are often the easiest attack vector  

---

##  Conclusion

This project demonstrates a structured penetration testing approach and highlights the importance of systematic reconnaissance, enumeration, exploitation, and privilege escalation.

The DoubleTrouble machine provided valuable hands-on experience in identifying and exploiting real-world vulnerabilities.
---

##  Author Information

**Author:** Jeevan Shaji John  
**Course:** BCA Cyber Security  
**Institution:** Marian College Kuttikkanam Autonomous  
**Year:** 2026
