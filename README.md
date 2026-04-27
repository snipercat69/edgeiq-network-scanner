# 🌐 EdgeIQ Network Scanner

**Pure Python network reconnaissance — no nmap required.**

Host discovery, TCP port scanning, service banner grabbing, and OS fingerprinting — all via Python sockets. Works on Linux, macOS, and Windows (WSL compatible).

[![Project Stage](https://img.shields.io/badge/Stage-Beta-blue)](https://edgeiqlabs.com)
[![Python](https://img.shields.io/badge/Python-3.8+-green)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-orange)](LICENSE)

---

## What It Does

Performs comprehensive **network reconnaissance** — host discovery via ICMP/TCP probe, TCP connect port scanning, service banner grabbing, and OS fingerprinting heuristics — **without nmap or any external dependencies**.

> ⚠️ **Legal Notice:** Only scan networks you own or have explicit written permission to audit. Unauthorized scanning is illegal.

---

## Key Features

- **Host Discovery** — ICMP ping sweep + TCP connect probe (works through firewalls)
- **TCP Port Scanning** — connect-scan with configurable depth (`quick` / `normal` / `intense`)
- **Banner Grabbing** — identify services and versions running on open ports
- **OS Fingerprinting** — heuristic detection based on open port patterns
- **Pure Python** — no nmap, no external dependencies
- **Cross-Platform** — Linux, macOS, Windows WSL fully supported
- **Concurrent Scanning** — multi-threaded for speed

---

## Prerequisites

- Python 3.8 or higher
- Network access to the target range
- **Written authorization** to scan the target network (required)

---

## Installation

```bash
# Clone the repo
git clone https://github.com/snipercat69/edgeiq-network-scanner.git
cd edgeiq-network-scanner

# No pip install needed — pure stdlib!
```

---

## Quick Start

### Quick Scan (9 common ports)
```bash
python3 scanner.py 192.168.1.0/24 quick
```

### Normal Scan (20 ports — recommended)
```bash
python3 scanner.py 192.168.1.0/24 normal
```

### Intense Scan (100 ports)
```bash
python3 scanner.py 192.168.1.0/24 intense
```

### Single Host
```bash
python3 scanner.py 10.0.0.1 normal
```

### Local Network Discovery
```bash
python3 scanner.py --local-scan
```

### Output Formats
```bash
python3 scanner.py 192.168.1.0/24 normal --format discord  # default
python3 scanner.py 192.168.1.0/24 normal --format json
python3 scanner.py 192.168.1.0/24 normal --format simple
```

---

## CLI Reference

| Flag | Type | Default | Description |
|------|------|---------|-------------|
| `target` | positional | — | IP, CIDR (e.g. `10.0.0.0/24`), hostname, or URL |
| `--depth` | choice | normal | Scan depth: `quick` (9 ports), `normal` (20), `intense` (100) |
| `--timeout` | float | 1.5 | Socket timeout in seconds |
| `--format` | choice | discord | Output format: `discord`, `json`, `simple` |
| `--local` | flag | False | Scan all detected local network ranges |
| `--local-scan` | flag | False | Fast scan: gateway + nearby IPs on your subnet |

---

## Scan Depth Levels

| Level | Ports Scanned | Best For |
|-------|--------------|----------|
| `quick` | 9 | Fast local discovery — SSH, HTTP, SMB, RDP |
| `normal` | 20 | General reconnaissance — adds DNS, SMTP, FTP, MySQL |
| `intense` | 100 | Full vulnerability assessment |

---

## Output Example

```
🔍 Scan Report — `192.168.1.0/24`
> Type: `full-normal` | Duration: 18.3s

🟢 192.168.1.1 — `router.local` 1.2ms
   └ OS: `Web-facing host`
   `   80` http         open — nginx
   `  443` https        open — nginx
   `8080` http-proxy    open — nginx

🟢 192.168.1.13 — `192.168.1.13` 8.7ms
   └ OS: `Windows (RDP + SMB)`
   `   80` http         open — Apache/Coyote 1.1
   ` 3389` ms-wbt-server open — Windows RDP

Hosts found: 2 | Ports scanned: 20 | Errors: 0
```

---

## Pricing

| Tier | Price | Features |
|------|-------|----------|
| **Free** | $0 | Host discovery, quick/normal/intense scan, 1 subnet |
| **Pro** | $20/mo | Autonomous subnet mapping, full /16 Class-B scanning, CVE correlation, Slack/Telegram delivery |
| **Lifetime** | $120 one-time | All Pro features, forever |

Get Pro via [EdgeIQ Labs](https://edgeiqlabs.com) — search "Network Scanner" in ClawHub.

---

## Integration with EdgeIQ Tools

Part of the **EdgeIQ Labs** security toolkit:
- **[EdgeIQ XSS Scanner](https://github.com/snipercat69/edgeiq-xss-scanner)** — after discovering web hosts, scan for XSS
- **[EdgeIQ SSL Watcher](https://github.com/snipercat69/edgeiq-ssl-watcher)** — monitor TLS on discovered HTTPS services
- **[EdgeIQ Subdomain Hunter](https://github.com/snipercat69/edgeiq-subdomain-hunter)** — expand enumeration to discover more attack surface

---

## Architecture

- **Language:** Python 3 (pure stdlib — no external packages)
- **Dependencies:** None (`socket`, `concurrent.futures`, `struct`, `ipaddress`)
- **Platforms:** Linux, macOS, Windows (WSL compatible)
- **Concurrency:** `concurrent.futures.ThreadPoolExecutor`

---

## Troubleshooting

**Q: Scanner reports "No live hosts found"**
A: The target may be firewalled or the subnet is wrong. Try `--local-scan` to auto-detect your subnet.

**Q: Slow scan results**
A: Increase socket timeout for faster host rejection: `--timeout 0.5`

**Q: Can I scan a URL like `https://example.com`?**
A: Yes — the scanner strips the protocol and resolves the hostname automatically.

---

## Legal & Ethical Use

This tool is for:
- Network administrators auditing their own infrastructure
- Penetration testers assessing client networks with authorization
- Bug bounty researchers (with program approval)
- Security researchers studying their own networks

This tool must NOT be used against networks without explicit written permission.

---

## Support

Open an issue at: https://github.com/snipercat69/edgeiq-network-scanner/issues

---

*Part of EdgeIQ Labs — [edgeiqlabs.com](https://edgeiqlabs.com)*
