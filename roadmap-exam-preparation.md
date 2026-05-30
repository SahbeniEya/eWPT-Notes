# eWPT Exam Preparation Roadmap 🗺️

> A structured learning path to prepare for the eWPT certification

---

## ⏱️ Suggested Timeline

```
Week 1-2  → Information Gathering & Recon
Week 3-4  → Web Application Analysis
Week 5-6  → Authentication & Session Testing
Week 7-8  → Injection Attacks (SQLi, XSS, CMDi)
Week 9-10 → File Upload, LFI/RFI, Traversal
Week 11   → API & Web Service Testing
Week 12   → Practice Labs & Mock Exam
```

---

## 📚 Learning Resources

### 🎓 Official Course
| Resource | Link | Priority |
|----------|------|----------|
| INE eWPT Course | [ine.com](https://ine.com) | ⭐⭐⭐⭐⭐ |

---

### 🔬 Practice Platforms

#### PortSwigger Web Security Academy
> Free, hands-on labs covering all web vulnerabilities

| Topic | Link |
|-------|------|
| All Labs | [portswigger.net/web-security](https://portswigger.net/web-security) |
| SQL Injection | [SQLi Labs](https://portswigger.net/web-security/sql-injection) |
| XSS | [XSS Labs](https://portswigger.net/web-security/cross-site-scripting) |
| Authentication | [Auth Labs](https://portswigger.net/web-security/authentication) |
| File Upload | [Upload Labs](https://portswigger.net/web-security/file-upload) |
| Path Traversal | [Traversal Labs](https://portswigger.net/web-security/file-path-traversal) |
| CSRF | [CSRF Labs](https://portswigger.net/web-security/csrf) |
| Session Security | [Session Labs](https://portswigger.net/web-security/oauth) |
| Business Logic | [Logic Labs](https://portswigger.net/web-security/logic-flaws) |
| SSRF | [SSRF Labs](https://portswigger.net/web-security/ssrf) |
| XXE | [XXE Labs](https://portswigger.net/web-security/xxe) |

---

#### HackTheBox Academy
> Structured learning paths with hands-on machines

| Path/Module | Link |
|-------------|------|
| Penetration Tester Path | [HTB Path](https://academy.hackthebox.com/app/paths/17/path-progress) |
| Web Attacks | [Web Attacks](https://academy.hackthebox.com/module/details/134) |
| File Inclusion | [LFI/RFI](https://academy.hackthebox.com/module/details/23) |
| SQL Injection | [SQLi](https://academy.hackthebox.com/module/details/33) |
| Session Security | [Sessions](https://academy.hackthebox.com/module/details/153) |
| Web Service & API | [API Testing](https://academy.hackthebox.com/module/details/160) |
| WordPress Attacks | [WP](https://academy.hackthebox.com/module/details/17) |
| XSS | [XSS](https://academy.hackthebox.com/module/details/103) |
| Information Gathering | [Recon](https://academy.hackthebox.com/module/details/144) |

---

#### TryHackMe
| Room | Link | Topic |
|------|------|-------|
| OWASP Top 10 | [THM](https://tryhackme.com/room/owasptop10) | All vulns |
| Web Fundamentals | [THM](https://tryhackme.com/room/webfundamentals) | Basics |
| OWASP Juice Shop | [THM](https://tryhackme.com/room/owaspjuiceshop) | Practice |
| SQL Injection | [THM](https://tryhackme.com/room/sqlilab) | SQLi |
| XSS | [THM](https://tryhackme.com/room/xssgi) | XSS |
| Burp Suite | [THM](https://tryhackme.com/room/burpsuitebasics) | Tool |

---

### 📖 Essential References

| Resource | Link | Use For |
|----------|------|---------|
| OWASP WSTG | [WSTG](https://owasp.org/www-project-web-security-testing-guide/) | Main methodology guide |
| OWASP Top 10 | [Top 10](https://owasp.org/www-project-top-ten/) | Vulnerability reference |
| PayloadsAllTheThings | [PATT](https://github.com/swisskyrepo/PayloadsAllTheThings) | Payloads & bypasses |
| HackTricks | [HackTricks](https://book.hacktricks.xyz) | Techniques & tips |
| CVE Details | [CVE](https://www.cvedetails.com) | CVE research |
| Exploit-DB | [EDB](https://www.exploit-db.com) | Public exploits |
| GTFOBins | [GTFOBins](https://gtfobins.github.io) | Binary exploitation |

---

## 📋 Domain-by-Domain Preparation

### Domain 1: Methodologies (10%)
```
✅ Read OWASP WSTG completely
✅ Understand penetration testing phases:
   → Recon → Scanning → Exploitation → Post-exploitation → Reporting
✅ Learn to write professional reports
```

**Resources:**
- [OWASP WSTG](https://owasp.org/www-project-web-security-testing-guide/)
- [PTES Standard](http://www.pentest-standard.org)

---

### Domain 2: Information Gathering (10%)
```
✅ Practice with: nmap, whois, dig, theHarvester
✅ Learn Google Dorking
✅ Practice subdomain enumeration
✅ Understand robots.txt, sitemap.xml
✅ Certificate transparency logs (crt.sh)
```

**Resources:**
- [HTB Information Gathering Module](https://academy.hackthebox.com/module/details/144)
- [Google Dorks DB](https://www.exploit-db.com/google-hacking-database)

---

### Domain 3: Web App Analysis (10%)
```
✅ Practice fingerprinting with: whatweb, wappalyzer, nmap
✅ Learn to identify CMS (WordPress, Joomla, Drupal)
✅ Understand HTTP methods and their risks
✅ Practice with gobuster and dirsearch
✅ Learn to read HTTP response headers
```

**Resources:**
- [HTB Web Attacks Module](https://academy.hackthebox.com/module/details/134)
- [Wappalyzer](https://www.wappalyzer.com)

---

### Domain 4: Vulnerability Assessment (15%)
```
✅ Practice testing default credentials
✅ Learn authentication bypass techniques
✅ Understand HTTP Auth types (Basic, Digest, Bearer)
✅ Practice with Hydra and Metasploit
✅ Learn to identify misconfigurations
```

**Resources:**
- [PortSwigger Authentication Labs](https://portswigger.net/web-security/authentication)
- [HTB Broken Authentication](https://academy.hackthebox.com)

---

### Domain 5: Security Testing (25%) ⭐ Most Important
```
✅ Directory Traversal → practice CVE-2021-41773
✅ File Upload → bypass filters, upload shells
✅ LFI/RFI → read files, achieve RCE
✅ Session Fixation → understand cookie handling
✅ Brute Force → Hydra, WPScan, custom scripts
✅ Command Injection → blind vs reflected
```

**Resources:**
- [PortSwigger File Upload Labs](https://portswigger.net/web-security/file-upload)
- [HTB File Inclusion Module](https://academy.hackthebox.com/module/details/23)
- [PortSwigger Path Traversal](https://portswigger.net/web-security/file-path-traversal)

---

### Domain 6: Manual Exploitation (20%)
```
✅ XSS → Reflected, Stored, DOM-based
✅ SQL Injection → Manual + SQLMap
✅ CMS Exploitation → WordPress, Joomla plugins
✅ Database extraction → credentials, sensitive data
```

**Resources:**
- [PortSwigger XSS Labs](https://portswigger.net/web-security/cross-site-scripting)
- [PortSwigger SQLi Labs](https://portswigger.net/web-security/sql-injection)
- [HTB SQL Injection Module](https://academy.hackthebox.com/module/details/33)

---

### Domain 7: Web Service Testing (10%)
```
✅ REST API enumeration
✅ Learn FastAPI, Flask API testing
✅ JWT token attacks
✅ BOLA/IDOR vulnerabilities
✅ Exposed sensitive endpoints
✅ TRACE method abuse
```

**Resources:**
- [HTB Web Service & API Module](https://academy.hackthebox.com/module/details/160)
- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/)

---

## 🎯 Practice Labs & CTF

| Platform | Focus | Link |
|----------|-------|------|
| DVWA | All web vulns | [DVWA](https://dvwa.co.uk) |
| OWASP Juice Shop | Modern web vulns | [Juice Shop](https://owasp.org/www-project-juice-shop/) |
| HackTheBox | Real machines | [HTB](https://hackthebox.com) |
| TryHackMe | Guided rooms | [THM](https://tryhackme.com) |
| VulnHub | Offline VMs | [VulnHub](https://vulnhub.com) |
| PentesterLab | Web specific | [PTL](https://pentesterlab.com) |

---

## 📝 Exam Tips

```
Before Exam:
→ Read all lab instructions carefully
→ Set up Burp Suite proxy
→ Prepare your notes and cheat sheet
→ Have wordlists ready (rockyou.txt, dirb/common.txt)

During Exam:
→ Start with full enumeration
→ Document every finding immediately
→ Don't skip any service or port
→ Check ALL HTTP methods on every endpoint
→ Look for default credentials first
→ Check source code for comments and secrets
→ Try directory traversal on ALL file parameters

Report Writing:
→ Include executive summary
→ Document all findings with screenshots
→ Provide clear reproduction steps
→ Rate severity (Critical/High/Medium/Low)
→ Include remediation recommendations
```

---

## ✅ Pre-Exam Checklist

```
□ Completed INE eWPT course
□ Practiced all PortSwigger labs
□ Completed HTB Penetration Tester path
□ Comfortable with Burp Suite
□ Can write SQL injection payloads manually
□ Understand XSS attack types
□ Practiced LFI/RFI exploitation
□ Know how to test file uploads
□ Understand session management attacks
□ Practiced API testing
□ Can write a professional pentest report
□ Reviewed OWASP WSTG checklist
```

---

<div align="center">

Good luck on your eWPT exam! 🚀

**[Back to README](./README.md)** | 
**[Cheat Sheet](./ewpt-cheat-sheet.md)**

</div>
