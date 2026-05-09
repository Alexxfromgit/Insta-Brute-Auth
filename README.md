# hacj

A Python-based credential testing tool for Instagram that uses wordlist attacks with automatic proxy rotation to avoid rate limiting.

> **Legal Notice:** Use this tool only on accounts you own or have explicit written authorization to test. Unauthorized use violates Instagram's Terms of Service and may be illegal under the Computer Fraud and Abuse Act (CFAA) or equivalent laws in your jurisdiction.

---

## Features

- Wordlist-based credential testing
- Automatic proxy discovery and rotation (via `proxybroker`)
- CSRF token extraction per login attempt
- Rate-limit detection with configurable cooldown
- Duplicate password filtering and UTF-8 wordlist support

## Requirements

- Python 3.6+
- [requests](https://pypi.org/project/requests/)
- [proxybroker](https://pypi.org/project/proxybroker/)
- [pysocks](https://pypi.org/project/PySocks/)

Install dependencies:

```bash
pip install requests proxybroker pysocks
```

## Usage

```bash
python data/hackinsta.py <username> <passwords_file>
```

| Argument          | Description                          |
|-------------------|--------------------------------------|
| `username`        | Target Instagram username            |
| `passwords_file`  | Path to a plaintext wordlist file    |

**Example:**

```bash
python data/hackinsta.py myaccount data/passwords.txt
```

## How It Works

1. **Proxy discovery** — Finds up to 20 working HTTP/HTTPS proxies at startup.
2. **User verification** — Confirms the target account exists before proceeding.
3. **Login loop** — Submits each password with a fresh CSRF token; exits immediately on success.
4. **Proxy rotation** — Switches proxy every 15 attempts.
5. **Rate-limit handling** — Detects `429` / checkpoint responses and pauses for 15 minutes before resuming.

## Configuration

Edit the constants at the top of `data/hackinsta.py`:

| Constant        | Default | Description                           |
|-----------------|---------|---------------------------------------|
| `DELAY_BETWEEN` | `4`     | Seconds between login attempts        |
| Proxy rotate    | `15`    | Attempts before switching proxy       |
| Rate-limit wait | `900`   | Seconds to wait on rate-limit (15 min)|

## Project Structure

```
hacj/
├── data/
│   ├── hackinsta.py    # Main script
│   └── passwords.txt   # Sample wordlist
└── README.md
```

## License

For educational and authorized security research use only.
