# 🔐 Penetration Testing Report – Footprinting & Network Scanning

**W2-PM-FINAL | Cybersecurity | Networkwalks**

## 📌 Project Information

| Field | Details |
|---|---|
| Pentester | Hamid |
| Program / Batch | B082 – Networkwalks |
| Date | 9 November 2026 |
| Program | Cybersecurity & Ethical Hacking |
| Modules | W2-PM1 – Multiple Kali Tools / W2-PM5 – Zenmap Scanning |
| Target | networkwalks.com and my own local LAN |
| Authorization | Written permission secured |
| Phases Covered | Reconnaissance, Footprinting, Scanning & Network Discovery |

---

## ⚠️ Liability Disclaimer

All activities documented in this repository were performed on systems for which written authorization was secured or on my own devices and network.

This project is intended for educational and research purposes only. Unauthorized access, scanning, or exploitation of systems is prohibited. The author, instructors, and Networkwalks are not responsible for any misuse of the information provided.

---

## 🎯 Project Overview

This project documents the practical exercises completed during Week 2 of the Networkwalks Cybersecurity Program.

The report covers two main phases:

- **Phase 1: Reconnaissance & Footprinting** – Gathering publicly available information about the `networkwalks.com` domain using Kali Linux tools.
- **Phase 2: Scanning & Network Discovery** – Identifying active devices on my own local LAN using Zenmap (Nmap GUI).

The objective was to understand how cybersecurity professionals gather information about a target, identify exposed technologies, enumerate DNS records, and discover active hosts within a network.

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| WHOIS | Domain registration information |
| WhatWeb | Website technology fingerprinting |
| Nslookup | DNS resolution |
| Curl | HTTP response header inspection |
| Wafw00f | Web Application Firewall detection |
| DNSRecon | DNS record enumeration |
| Zenmap | Network scanning and host discovery |
| Windows CMD | Local IP and subnet identification |
| Kali Linux | Reconnaissance environment |

---

## 🔎 Phase 1: Footprinting & Reconnaissance

### 1. WHOIS – Domain Information

**Command:**

```bash
whois networkwalks.com
```

**Key Findings:**
- Registrar: GoDaddy.com, LLC
- Domain Creation: 6 November 2019
- Domain Expiration: 6 November 2027
- Name Servers: NS6135.HOSTGATOR.COM, NS6136.HOSTGATOR.COM
- DNSSEC: Unsigned
- Registrant privacy service: Domains By Proxy, LLC

### 2. WhatWeb – Technology Fingerprinting

**Command:**

```bash
whatweb networkwalks.com
```

**Key Findings:**
- Web Server: Apache
- CMS: WordPress 7.1.4
- Plugin: WordPress Download Manager 3.3.76
- Bootstrap: 7.1.4
- jQuery: 3.7.1
- IP Address: 192.232.216.135
- Website Title: Networkwalks Academy
- Google Tag Manager detected

### 3. Nslookup – DNS Resolution

**Command:**

```bash
nslookup networkwalks.com
```

**Key Finding:**

```text
networkwalks.com → 192.232.216.135
```

### 4. Curl – HTTP Headers

**Command:**

```bash
curl -I https://networkwalks.com
```

**Key Findings:**
- HTTP Status: HTTP/2 200
- Server: Apache
- WordPress REST API endpoint: `/wp-json/`
- WordPress page endpoint: `/wp-json/wp/v2/pages/53`
- X-Nginx-Cache: WordPress
- Secure and HttpOnly cookie attributes observed

### 5. Wafw00f – WAF Detection

**Command:**

```bash
wafw00f networkwalks.com
```

**Key Finding:**

```text
Web Application Firewall: ModSecurity (SpiderLabs)
```

### 6. DNSRecon – DNS Enumeration

**Command:**

```bash
dnsrecon -d networkwalks.com
```

**Key Findings:**
- SOA Record: ns6135.hostgator.com
- NS Records: ns6135.hostgator.com, ns6136.hostgator.com
- A Record: 192.232.216.135
- MX Record: mail.networkwalks.com
- SPF Record identified
- Google Site Verification TXT record identified
- SRV records for cPanel email discovery identified
- BIND Version: 9.16.23-RH
- DNSSEC query returned no answer

---

## 🌐 Phase 2: Network Scanning & Discovery

### Local Network Configuration

**Command:**

```cmd
ipconfig
```

| Field | Value |
|---|---|
| IPv4 Address | 192.168.28.21 |
| Subnet Mask | 255.255.255.0 |
| Network Subnet | 192.168.28.0/24 |

### Zenmap Ping Scan

**Scan Type:** Ping Scan

**Network:** `192.168.28.0/24`

**Results:**
- Total IP Addresses Scanned: 256
- Live Hosts Discovered: 8
- Scan Duration: 5.48 seconds

### Discovered Hosts

| No. | IP Address | MAC Address | Vendor |
|---|---|---|---|
| 1 | 192.168.28.1 | B4:63:6F:B0:0F:D0 | Nokia Solutions and Networks |
| 2 | 192.168.28.2 | C2:B0:30:87:39:DF | Unknown |
| 3 | 192.168.28.4 | 42:DC:BC:01:86:42 | Unknown |
| 4 | 192.168.28.7 | 7C:EC:B1:63:CA:F5 | Apple |
| 5 | 192.168.28.14 | AE:96:BB:C8:98:93 | Unknown |
| 6 | 192.168.28.23 | CA:80:BD:BD:65:D8 | Unknown |
| 7 | 192.168.28.67 | 0E:D9:04:CF:9E:65 | Unknown |
| 8 | 192.168.28.21 | Not listed | My PC |

---

## 📊 Risk Analysis

| Finding | Potential Impact | Risk Level |
|---|---|---|
| WordPress and plugin version exposed | May assist vulnerability research | Medium |
| Server IP address identifiable | Reveals network location | Low |
| HTTP technical information exposed | May assist further enumeration | Low |
| ModSecurity WAF identifiable | Reveals security architecture | Low |
| DNS infrastructure information exposed | Helps build infrastructure profile | Medium |
| DNSSEC unsigned | DNS authenticity protection may be reduced if DNSSEC is required | Low |
| Multiple live hosts discovered | Unknown devices may require investigation | Medium |
| Unknown MAC vendors identified | Device identification may be incomplete | Low |

**Note:** These are potential risks based on reconnaissance and scanning observations. No exploitation or vulnerability validation was performed.

---

## 🛡️ Recommendations

1. Review publicly exposed web technologies and software versions.
2. Keep WordPress, plugins, and web server components updated.
3. Review HTTP response headers for unnecessary information disclosure.
4. Regularly audit DNS records and configurations.
5. Properly configure and monitor ModSecurity.
6. Review DNSSEC configuration and enable it where appropriate.
7. Perform regular internal network discovery.
8. Investigate unknown devices within the network.
9. Maintain updated network topology and asset documentation.
10. Ensure all security testing is performed with proper authorization.

---

## 📸 Evidence

The following evidence was collected during the practical exercises:

- WHOIS domain registration output
- WhatWeb technology fingerprinting output
- Nslookup DNS resolution output
- Curl HTTP response headers
- Wafw00f WAF detection output
- DNSRecon DNS enumeration output
- Windows `ipconfig` output
- Zenmap Ping Scan results
- Zenmap network topology

---

## 📚 Learning Outcomes

Through this practical exercise, I gained hands-on experience in:

- Performing domain footprinting and reconnaissance.
- Identifying web technologies and CMS platforms.
- Enumerating DNS records and infrastructure.
- Inspecting HTTP response headers.
- Detecting Web Application Firewalls.
- Identifying live hosts within a local network.
- Collecting IP and MAC address information.
- Understanding the importance of authorization and ethical security testing.
- Documenting cybersecurity findings in a structured report.

---

## 🏁 Conclusion

This Week 2 practical exercise helped me develop a better understanding of reconnaissance, footprinting, and network scanning.

By using Kali Linux tools and Zenmap, I collected information about a target domain and discovered active devices within my local network.

The practical demonstrated how information gathering plays an important role in cybersecurity assessments and how collected information can help security professionals understand an environment before performing further authorized testing.

---

**Author:** Hamid  
**Program:** Cybersecurity & Ethical Hacking  
**Batch:** B082 – Networkwalks

**Project:** Networkwalks Cybersecurity Program – Week 02  
**Modules:** W2-PM1 & W2-PM5
