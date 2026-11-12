# Reconnaissance & Scanning Command Reference

## Module W2-PM1: Kali Linux Footprinting Tools
```bash
# 1. Domain registration & name server lookup
whois networkwalks.com

# 2. Web technology & CMS fingerprinting
whatweb networkwalks.com

# 3. DNS A-record IP resolution
nslookup networkwalks.com

# 4. HTTP response header & endpoint inspection
curl -I [https://networkwalks.com](https://networkwalks.com)

# 5. Web Application Firewall (WAF) detection
wafw00f networkwalks.com

# 6. Full DNS record enumeration (SOA, NS, MX, TXT, SRV)
dnsrecon -d networkwalks.com


Module W2-PM2: Google Hacking Database (GHDB) Dorks
intitle:"Webcam" inurl:WebCam.htm
inurl:webcam site:skylinewebcams.com inurl:roma
Camera Live Image inurl:guestimage.html
Module W2-PM4: theHarvester OSINT Enumeration
# Multi-source passive enumeration
theHarvester -d microsoft.com -l 1000 -b all

# Targeted search engine enumeration
theHarvester -d microsoft.com -l 1000 -b baidu

Module W2-PM5: Network Discovery (Windows CMD & Zenmap / Nmap)
DOS
:: Identify local IP address and subnet mask on Windows
ipconfig
Bash
# Ping sweep across local /24 subnet to identify live hosts & MAC addresses
nmap -sn 192.168.0.112/24
4. Click **Commit changes...**[cite: 1]

---

### Step 5: Add the License (`LICENSE`)
1. Click **Add file** -> **Create new file**[cite: 1].
2. In the file name box, type: `LICENSE`[cite: 1].
3. Copy and paste the license text below[cite: 1]:

```text
MIT License

Copyright (c) 2026 Karam Alwakeel



