# Penetration Testing Report: Footprinting & Network Scanning Phases

**Program:** Networkwalks Cybersecurity & Ethical Hacking Program (B082-Networkwalks)  
**Author:** Karam Alwakeel  
**Date:** November 12, 2026  
**Report ID:** W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS  

---

## Overview
This repository documents the practical assessments, methodology, findings, risk analysis, and remediation recommendations from **Week 02** of the Cybersecurity & Ethical Hacking Internship. It covers **Phase 1 (Reconnaissance & Footprinting)** and **Phase 2 (Scanning & Network Discovery)** executed against authorized targets (`networkwalks.com` and a local LAN environment).

## Repository Structure
```text
networkwalks-penetration-testing-week2/
├── README.md                          # Project overview, metadata, and quick start
├── LICENSE                            # MIT License
├── .gitignore                         # Standard Git ignore rules
├── docs/
│   └── PENETRATION_TESTING_REPORT.md  # Complete, full-text penetration testing report
└── references/
    └── commands.md                    # Exact commands used across all 5 modules


**Program:** Networkwalks Cybersecurity & Ethical Hacking Program (B082-Networkwalks)  
**Author:** Karam Alwakeel  
**Pentester (Report Attribution):** Emmanuel John  
**Date:** November 12, 2026  
**Report ID:** W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS  

** 02 | **Repository:** GitHub
| Field | Details |
|---|---|
| **Pentester Name (Cybersecurity Professional)** | Emmanuel John |
| **Author** | Karam Alwakeel |
| **Program / Batch** | B082-Networkwalks |
| **Date** | 12 Nov 2026 |
| **Modules Completed** | W2-PM1 (Multiple Kali Tools)<br>W2-PM2 (GHDB)<br>W2-PM3 (Maltego)<br>W2-PM4 (The Harvester)<br>W2-PM5 (Zenmap Scanning) |
| **Client / Target** | 1. Networkwalks (secured written permission already)<br>2. My own local LAN Network |
| **Permission Secured from Client?** | Yes |
| **Phases Covered** | Phase 1: Reconnaissance & Footprinting<br>Phase 2: Scanning & Network Discovery<br>Phase 3-5: In Progress |

---

## 1. Liability Disclaimer
I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.

## 2. Introduction
This report covers footprinting where I used multiple tools to perform active and passive reconnaissance using multiple tools to see if there are any vulnerabilities that could be found. The tools that were used were:
1. Multiple Kali Linux commands to find out information about the target.
2. The Google Hacking Database (GHDB), which is a form of active reconnaissance looking for publicly available data about the target.
3. Maltego for OSINT gathering and entity visualization.
4. The Harvester tool in Kali Linux.
5. Zenmap, the graphical interface of Nmap, on a Windows machine for the scanning phase.

Every step below includes the exact command used, the result I observed, and a short note on why the finding matters from an attacker's point of view.

## 3. Tools Used
| Tool | Purpose |
|---|---|
| **Kali Linux & Windows** | Operating systems used for reconnaissance activities |
| **WHOIS** | Find domain registration details (owner, dates, name servers) |
| **whatweb** | Fingerprint web technologies (server, CMS, plugins, IP) |
| **nslookup** | Resolve the domain name to its IP address using DNS |
| **curl -I** | Read the HTTP response headers of the website |
| **wafw00f** | Detect whether a Web Application Firewall protects the site |
| **dnsrecon** | Enumerate all DNS records (NS, MX, SPF, TXT, SRV) |
| **Zenmap (Nmap GUI)** | Scan the local subnet to find live hosts, IPs and MAC addresses |
| **Windows CMD** | Local IP and MAC address identification |
| **Maltego** | Open-source intelligence (OSINT) gathering, network analysis, and visualizing relationships between digital entities to uncover hidden connections |
| **The Harvester** | Footprinting tool used for gathering information of emails, sub-domains, hosts, employee names, open ports and banners from different public sources like search engines |
| **GHDB** | OSINT used to find publicly listed information such as cameras that are not secured |

---

## 4. Activities Performed

### 4.1 Footprinting & Reconnaissance
I performed reconnaissance against the `networkwalks.com` domain using six Kali Linux tools: WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon. Each tool was used to collect a different type of information about the target.

* **WHOIS (`whois networkwalks.com`):** Obtained publicly available domain registration information (Registrar: GoDaddy.com, LLC; Created: 2019-11-06; Expires: 2027-11-06) and identified the domain's name servers (`NS6135.HOSTGATOR.COM`, `NS6136.HOSTGATOR.COM`).
* **WhatWeb (`whatweb networkwalks.com`):** Identified technologies used by the website, including **WordPress 7.1.4**, **Apache**, **Bootstrap 7.1.4**, **jQuery 3.7.1**, **WP Download Manager 3.3.76**, and contact email `info@networkwalks.com`.
* **Nslookup (`nslookup networkwalks.com`):** Resolved the domain name to its IP address: `192.232.216.135`.
* **Curl (`curl -I https://networkwalks.com`):** Inspected the HTTP/2 200 response headers, exposing server details (`Apache`), caching headers (`x-nginx-cache: WordPress`), and the WordPress REST API endpoint `/wp-json/`.
* **Wafw00f (`wafw00f networkwalks.com`):** Determined whether a Web Application Firewall was protecting the website, identifying **ModSecurity (SpiderLabs)**.
* **DNSRecon (`dnsrecon -d networkwalks.com`):** Enumerated DNS records including SOA, NS (`ns6135.hostgator.com`, `ns6136.hostgator.com`), Bind versions (`9.16.23-RH`), MX (`mail.networkwalks.com`), SPF/TXT records, and SRV `_autodiscover._tcp` records.

### 4.2 OSINT with GHDB
Used the Google Hacking Database (Exploit-DB) to locate publicly exposed cameras and devices using Google dorks:
* `intitle:"Webcam" inurl:WebCam.htm`
* `inurl:webcam site:skylinewebcams.com inurl:roma`
* `Camera Live Image inurl:guestimage.html`

### 4.3 OSINT using Maltego
Conducted passive OSINT gathering against `networkwalks.com` using Maltego Desktop 4.14.0. By querying public search engines, DNS records, and indexed web repositories via automated transforms, identified publicly exposed organizational email address `info@networkwalks.com` without directly alerting the target's mail servers.

### 4.4 The Harvester Tool
Executed passive OSINT enumeration against `microsoft.com` using `theHarvester` (v4.10.1) in Kali Linux (`theHarvester -d microsoft.com -l 1000 -b all` and `-b baidu`) to harvest publicly exposed emails, sub-domains, and host records across unauthenticated OSINT sources.

### 4.5 Network Scanning with Zenmap
Used Windows `ipconfig` to identify the local IP address and LAN subnet, then performed a Zenmap Ping Scan (`nmap -sn 192.168.0.112/24`) to discover live hosts, IP addresses, and MAC addresses (identifying vendors including ZTE, Amazon Technologies, and Samsung Electronics), and exported the Zenmap network topology in PDF format.

---

## 5. Risk Analysis / Impact
Based on the information collected during the footprinting and network scanning activities, the following potential risks were identified:

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
|---|---|---|---|---|
| 1 | Web technology information exposed | WhatWeb identified WordPress and WP Download Manager | Attackers may use exposed technology/version information to identify software requiring further security review | ● Medium |
| 2 | Server IP address identifiable | Nslookup resolved the domain to `192.232.216.135` | Provides information about the network location of the web service | ● Low |
| 3 | HTTP technical information exposed | Curl returned HTTP response headers and exposed `/wp-json/` | May assist technology fingerprinting and further enumeration | ● Low |
| 4 | WAF technology identifiable | Wafw00f identified ModSecurity (SpiderLabs) | Reveals information about the web application's security architecture | ● Low |
| 5 | DNS infrastructure information exposed | DNSRecon identified DNS, mail and service-related records | DNS information can help build a broader infrastructure profile | ● Medium |
| 6 | Multiple live hosts visible on local network | Zenmap identified 5+ live hosts in the local subnet | Unknown or unauthorized devices may potentially be present on a network | ● Medium |

*Risk level key: ● Critical ● Medium ● Low*

> **Note:** The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities. No exploitation or vulnerability validation was performed as part of these two modules. Further authorized security testing would be required to confirm any actual vulnerability.

---

## 6. Recommendations
1. **Review publicly exposed technology information:** Organizations should regularly review what information about their web technologies, CMS and plugins is publicly visible.
2. **Keep software updated:** CMS platforms, plugins and other web technologies should be regularly updated and reviewed against current security advisories.
3. **Review HTTP headers:** HTTP response headers should be reviewed to determine whether unnecessary technical information is being exposed.
4. **Review DNS records regularly:** DNS records should be checked periodically to ensure that only required information and services are publicly exposed.
5. **Properly configure and monitor the WAF:** Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks.
6. **Perform regular internal network discovery:** Organizations should periodically scan their own networks to identify active devices.
7. **Investigate unknown devices:** Any unexpected device discovered during network scanning should be investigated and verified.
8. **Maintain network documentation:** Network topology and device information should be documented and updated regularly.
9. **Perform security testing with authorization:** Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided.

---

## 7. Conclusion
During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance and network scanning.

In the footprinting activity, I used six Kali Linux tools to collect information about the target domain (`WHOIS`, `WhatWeb`, `Nslookup`, `Curl`, `Wafw00f`, and `DNSRecon`). In the network scanning activity, I used Zenmap to identify my local network configuration, discover active hosts, collect IP and MAC address information, and create a network topology.

The exercises demonstrated that information gathering is a critical phase of cybersecurity, technical findings must be documented clearly with risk context and remediation steps, and reconnaissance and scanning must always remain strictly within an authorized scope.

---
**Author:** Karam Alwakeel  
**Program Name:** Cybersecurity program at Networkwalks | **Week:** 02 | **Repository:** GitHub
