# OSINT Board

An interactive investigation board that visualises how digital forensic analysts and OSINT investigators map a target's online footprint. Enter an IP address, domain, email, or username — the board fans out like a cork board, with each card representing a real investigative finding.

Built as a learning tool for blue team cybersecurity and digital forensics methodology.

![osint-board-preview](preview.png)

---

## Live Demo

Open `osint-board-live.html` directly in your browser. No server required for the live API features.

---

## What It Does

You enter a target and the board populates with connected nodes — each one representing something a real investigator would discover. Cards are colour-coded by data source:

- 🟢 **Green stripe** — live data from a real API call
- 🟡 **Yellow stripe** — simulated / educational data
- 🔴 **Red stripe** — API error or missing key

Click any card to open the detail panel, which shows the full data returned and explains the real OSINT technique used at that step, including which tools investigators actually use.

---

## Data Sources

| Target Type | Data | Source | Key Required |
|-------------|------|--------|-------------|
| IP Address | Geolocation, ASN, ISP, Timezone | ipinfo.io | No |
| IP Address | Reverse DNS (PTR record) | Google DNS | No |
| IP Address | Threat reputation, blocklists | AbuseIPDB | Free account |
| IP Address | Open ports / services | Shodan | Paid (simulated) |
| Domain | Subdomains, SSL certificates | crt.sh | No |
| Domain | DNS A, MX, TXT records | Google DNS | No |
| Domain | Server geolocation | ipinfo.io | No |
| Domain | WHOIS registration | CLI / terminal | No |
| Email | Data breach history | HaveIBeenPwned | Paid (~$3.50/mo) |
| Email | Platform enumeration | Simulated | — |
| Username | Platform enumeration | Simulated | — |

> **Note:** Platform username checks (Sherlock-style) are simulated — browser-based probing is blocked by CORS on most platforms. For real username enumeration, run [Sherlock](https://github.com/sherlock-project/sherlock) locally.

---

## Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/yourusername/osint-board.git
cd osint-board
```

### 2. Open in browser
```bash
open osint-board-live.html
# or just double-click the file
```

No build step, no dependencies, no server required.

### 3. Try it immediately (no keys needed)

- `8.8.8.8` — Google's DNS server. Live geolocation, ASN, reverse DNS.
- `1.1.1.1` — Cloudflare DNS. Same live data.
- `github.com` — Real subdomain enumeration via crt.sh, live DNS records.
- `cloudflare.com` — Large cert footprint, many subdomains.

### 4. Add API keys for more live data (optional)

Click **⚙ API KEYS** in the top bar.

**AbuseIPDB** (free)
1. Create a free account at [abuseipdb.com](https://www.abuseipdb.com)
2. Go to Account → API → Create Key
3. Paste into the API Keys panel

**HaveIBeenPwned** (paid, ~$3.50/month)
1. Get a key at [haveibeenpwned.com/API/Key](https://haveibeenpwned.com/API/Key)
2. Paste into the API Keys panel
3. Now email lookups return real breach data

> Keys are stored in browser memory only — they are never sent anywhere except the respective API.

---

## What You Learn

Working through this tool covers the following concepts:

**Passive Reconnaissance**
Everything in this tool is passive — no direct contact with the target. All queries go to third-party databases (crt.sh, ipinfo.io, HIBP), not the target itself. This is a fundamental operational security distinction.

**Certificate Transparency**
crt.sh logs every SSL certificate ever issued. Querying it passively reveals subdomains without touching the target's infrastructure.

**IP Intelligence**
GeoIP, ASN lookup, reverse DNS, and reputation feeds each answer a different question: *Where is this server? Who owns it? What's it called? Has it been used maliciously?*

**Breach Data**
HIBP aggregates hundreds of data breaches. A match reveals what credentials were exposed — and whether they're likely in active credential stuffing lists.

**DNS as Evidence**
MX records reveal email providers. TXT records expose SPF/DMARC policies and third-party service integrations. These are often overlooked but highly informative.

---

## MITRE ATT&CK Mapping

This tool covers the **Reconnaissance** tactic (TA0043):

| Technique | ID |
|-----------|-----|
| Search Open Websites/Domains | T1593 |
| Search Open Technical Databases | T1596 |
| Gather Victim Identity Information | T1589 |
| Gather Victim Network Information | T1590 |
| Gather Victim Org Information | T1591 |

---

## Limitations

- **CORS** — Some APIs block direct browser requests. In production, route queries through a backend proxy.
- **Rate limits** — ipinfo.io free tier: 50,000 requests/month. AbuseIPDB free: 1,000/day. HIBP: 1 request/1500ms.
- **Legal** — This tool is for educational use and authorised investigations only. Do not use against targets you do not have permission to investigate.

---

## Roadmap

- [ ] Backend proxy to resolve CORS limitations
- [ ] Shodan integration for real port/service data
- [ ] Export board as PDF investigation report
- [ ] Maltego-style graph layout engine
- [ ] WHOIS live via whoisjson.com
- [ ] VirusTotal domain/IP reputation

---

## Built With

- Vanilla HTML / CSS / JavaScript — no frameworks, no build tools
- [ipinfo.io](https://ipinfo.io) — IP geolocation and ASN
- [crt.sh](https://crt.sh) — Certificate transparency logs
- [Google DNS over HTTPS](https://dns.google) — DNS record resolution
- [AbuseIPDB](https://www.abuseipdb.com) — IP threat intelligence
- [HaveIBeenPwned](https://haveibeenpwned.com) — Breach database

---

## Disclaimer

This tool is intended for educational purposes and authorised security research only. Always ensure you have explicit permission before investigating any target. The author is not responsible for misuse.

---

## License

MIT
```

---

**Topics to add on GitHub** (goes in the repo settings under Topics):
```
osint  digital-forensics  blue-team  cybersecurity  threat-intelligence  
reconnaissance  ctf  security-research  educational
