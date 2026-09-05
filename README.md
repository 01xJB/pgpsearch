<div align="center">

# PGPSearch

**Harvest publicly listed PGP identities for any domain, straight from the keyserver network**

![License](https://img.shields.io/github/license/01xJB/pgpsearch?color=blue&style=for-the-badge)
![Version](https://img.shields.io/badge/version-1.5.0-success?style=for-the-badge)
![Python](https://img.shields.io/badge/python-3.7+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Status](https://img.shields.io/badge/status-active-brightgreen?style=for-the-badge)

</div>

---

## Overview

PGPSearch queries the Ubuntu PGP keyserver for a given domain and extracts every publicly listed name/email pair associated with it. It's a lightweight OSINT primitive: a fast way to build an initial email/identity list for a target organization from data people have already chosen to publish on a public keyserver. Useful for recon, attack-surface mapping, or auditing your own org's exposure.

## Features

- 🔍 **Domain-scoped lookup** against the Ubuntu keyserver (`keyserver.ubuntu.com`)
- ⚡ **Multi-threaded execution** for faster bulk queries
- 🧾 **Two output formats**: a readable name+email table, or a plain email-only list
- 🌐 **Proxy support** (`socks5://`, `http://`, …) for privacy-conscious lookups
- 💾 **File export** alongside console output

## Requirements

- Python 3.7+
- Dependencies in [`requirements.txt`](requirements.txt) (`requests`, `beautifulsoup4`, `rich`)

## Installation

```bash
git clone https://github.com/01xJB/pgpsearch.git
cd pgpsearch
pip install -r requirements.txt
```

## Usage

```bash
python3 pgpsearch.py -d <domain> [-t <threads>] [--proxy <proxy>] [-o <output_file>] [-f <format>]
```

| Flag | Required | Description |
|---|---|---|
| `-d`, `--domain` | ✅ | Domain to search for associated PGP identities |
| `-t`, `--threads` | | Number of concurrent lookups (default: `1`) |
| `--proxy` | | Proxy URL, e.g. `socks5://127.0.0.1:9050` |
| `-o`, `--output` | | File to write results to |
| `-f`, `--format` | | Output format: `default` (table) or `email` (default: `default`) |

### Example

Fetch identities for `example.com` with 5 threads, saving email-only results:

```bash
python3 pgpsearch.py -d example.com -t 5 -o emails.txt -f email
```

```
┏━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Name            ┃ Email                    ┃
┡━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ <Jane Doe>      │ jane.doe@example.com     │
│ <John Smith>    │ john.smith@example.com   │
└─────────────────┴──────────────────────────┘
```

## Output Formats

| Format | Description |
|---|---|
| `default` | Name + email in a rendered table (also written to file if `-o` is set) |
| `email` | Email addresses only, one per line |

## Contributing

Issues and pull requests are welcome. Open one to discuss a change before submitting.

## License

Released under the [MIT License](LICENSE).

---

<div align="center">

Built by [**01xJB**](https://github.com/01xJB)

</div>
