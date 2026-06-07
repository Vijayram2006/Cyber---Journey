NETWORK SECURITY ASSESSMENT REPORT
---
Executive Summary
Target Host: 192.168.234.129 (Metasploitable)  
Scan Date: Jun 5, 2026  
Security Analyst: Vijayram K  
Assessment Type: Full Network Reconnaissance & Vulnerability Identification  
Risk Level: 🔴 CRITICAL
---
1. Scanning Methodology
Tools Used
Nmap 7.x — Network Mapper
Service Detection: nmap -sV
OS Detection: nmap -O
Aggressive Scan: nmap -A
Scan Parameters
```
nmap -sV 192.168.234.129          [Service & Version Detection]
nmap -O 192.168.234.129            [OS Identification]
nmap -A 192.168.234.129            [Full Aggressive Scan]
nmap -sV -p 21,22,80 192.168.234.129 [Targeted Port Scan]
```
Scan Results
Total Ports Scanned: 1000
Open Ports Found: 24
Host Status: UP (0.080s latency)
Scan Duration: ~50.03 seconds
---
2. Host Information
Detail	Value
IP Address	192.168.234.129
Operating System	Linux (Debian/Ubuntu based)
Hostname	metasploitable.localdomain
MAC Address	00:0C:29:FA:DD:2A
Network Interface	eth0
---
3. Open Ports & Services Discovered
Critical Risk Services (🔴 CRITICAL)
Port	Protocol	Service	Version	CVE Status	Risk Level
21	TCP	FTP	vsftpd 2.3.4	CVE-2011-2523	🔴 CRITICAL
23	TCP	Telnet	Linux telnetd	Multiple	🔴 CRITICAL
80	TCP	HTTP	Apache 2.2.8	Multiple	🔴 CRITICAL
3306	TCP	MySQL	5.0.51a	Multiple	🔴 CRITICAL
5900	TCP	VNC	3.3	Weak Auth	🔴 CRITICAL
High Risk Services (🟡 HIGH)
Port	Protocol	Service	Version	Issue
22	TCP	SSH	OpenSSH 4.7p1	Outdated
25	TCP	SMTP	Postfix smtpd	Mail Relay
53	TCP	Domain	ISC BIND 9.4.2	DNS
111	TCP	rpcbind	2-4	RPC exposure
139	TCP	netbios-ssn	Samba smbd 3.x	SMB
445	TCP	netbios-ssn	Samba smbd 3.x	SMB
512	TCP	exec	rsh exec	Remote shell
513	TCP	login	rsh	Rlogin
514	TCP	shell	rsh	Remote shell
1099	TCP	java-rmi	Java RMI	RMI Registry
1524	TCP	bindshell	Metasploitable shell	Backdoor
2049	TCP	nfs	NFS	NFS exposure
2121	TCP	ftp	ProFTPD 1.3.1	FTP
3632	TCP	distcc	Distcc v1	Code Execution
5432	TCP	postgresql	8.3.0-8.3.7	Database
5984	TCP	couchdb	CouchDB	NoSQL
6667	TCP	irc	UnrealIRCd	IRC Server
6697	TCP	ajp13	Tomcat JSP	Tomcat
8180	TCP	http	Tomcat/Coyote	Web Server
8787	TCP	drb	Ruby DRb	Code Execution
---
4. Vulnerability Assessment
vsftpd 2.3.4 Backdoor (Port 21) — CRITICAL
CVE ID: CVE-2011-2523  
CVSS Score: 9.8 (CRITICAL)  
Description: vsftpd version 2.3.4 contains a backdoor that allows remote code execution with root privileges.
Impact:
Remote attacker can gain complete system access
Root-level command execution possible
No authentication required
Affected Version: vsftpd 2.3.4  
Status: 🔴 EXPLOITABLE
Exploit Framework: Metasploit  
`exploit/unix/ftp/vsftpd_234_backdoor`
---
Telnet Service (Port 23) — CRITICAL
Issue: Unencrypted remote login service  
Risk: All credentials transmitted in plaintext  
Status: 🔴 UNENCRYPTED
---
Apache 2.2.8 (Port 80) — HIGH
CVE IDs: Multiple (CVE-2011-3192, CVE-2011-3368, etc.)  
Description: Outdated Apache version with known vulnerabilities
Potential Attacks:
Directory traversal
Cross-site scripting (XSS)
Request smuggling
Status: 🟡 EXPLOITABLE
---
MySQL 5.0.51a (Port 3306) — HIGH
Issue: Unauthenticated or weak authentication possible  
Risk: Database access without credentials  
Status: 🟡 EXPLOITABLE
---
VNC Server (Port 5900) — HIGH
Version: 3.3  
Issue: Weak authentication mechanism  
Risk: Remote desktop access possible  
Status: 🟡 EXPLOITABLE
---
5. Attack Surface Analysis
Immediate Exploitation Path
```
1. Port 21 (vsftpd 2.3.4)
   ↓
   Exploit: CVE-2011-2523 Backdoor
   ↓
   Result: ROOT SHELL ACCESS ✓

2. Port 80 (Apache 2.2.8)
   ↓
   Exploit: Web vulnerabilities
   ↓
   Result: Web shell / Data breach

3. Port 3306 (MySQL)
   ↓
   Exploit: SQL injection / Weak auth
   ↓
   Result: Database compromise

4. Port 5900 (VNC)
   ↓
   Exploit: Authentication bypass
   ↓
   Result: Remote desktop control
```
---
6. Exploitation Recommendations
Primary Target: vsftpd 2.3.4
Command:
```bash
msfconsole
search vsftpd 2.3.4
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.234.129
run
```
Expected Result: Root shell with UID=0
---
7. Risk Assessment Summary
Severity Breakdown
🔴 CRITICAL: 5 services
🟡 HIGH: 19 services
🟠 MEDIUM: 0 services
🟢 LOW: 0 services
Overall Security Posture
Status: ⛔ CRITICALLY COMPROMISED
Recommendation: System should NOT be accessible from any network unless isolated for authorized penetration testing.
---
8. Conclusion
The target host (192.168.234.129) presents an extremely high security risk with multiple critical vulnerabilities that can lead to complete system compromise. The vsftpd 2.3.4 backdoor provides a direct path to root-level access.
Immediate Actions Required:
✓ Isolate system from production network
✓ Update all services to latest versions
✓ Implement access controls
✓ Enable encryption (SSH instead of Telnet)
✓ Deploy intrusion detection systems
---
Report Metadata
Field	Value
Analyst Name	Vijayram K
Report Date	Jun 5, 2026
Target System	Metasploitable 2
Assessment Level	Full Network Reconnaissance
Confidentiality	Internal Use Only
---
Report Generated By: Security Assessment Team  
Status: ✅ COMPLETE  
Next Phase: Exploitation & Post-Exploitation Analysis
---
Appendix — Scan Output
```
Host is up (0.080s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8
111/tcp  open  rpcbind     2-4
139/tcp  open  netbios-ssn Samba smbd 3.x-4.x
445/tcp  open  netbios-ssn Samba smbd 3.x-4.x
512/tcp  open  exec        rsh
513/tcp  open  login       rsh
514/tcp  open  shell       rsh
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
3632/tcp open  distcc      distcc v1
5432/tcp open  postgresql  PostgreSQL DB 8.3.0-8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6667/tcp open  irc         UnrealIRCd
6697/tcp open  ajp13       Apache Jserv
8180/tcp open  http        Apache Tomcat/Coyote JSP
8787/tcp open  drb         Ruby DRb
```
---
END OF REPORT
