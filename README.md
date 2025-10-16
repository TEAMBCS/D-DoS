<p align="center">
  <img src="https://i.postimg.cc/htzxw4kF/D-DoS.jpg" width="600"/>
</p>

<h1 align="center"> HTTPS Flood DDoS Tool</h1>

<p align="center">
  🚀 Powered by <b> BANGLADESH CYBER SQUAD </b><br>
  📆 Year: 2025
</p>

# HTTPS Flood [bold yellow]Info

**A fast, mobile-aware HTTP/HTTPS flood tool (for authorized testing only)**

> HTTPS Flood V1 is a load-generation tool designed for security testing and resilience checks on systems you own or have explicit written permission to test. It simulates realistic mobile traffic by randomizing headers, cookies, query strings and payloads. The script includes adaptive threading tuned for Android/Termux and produces simple runtime statistics and breakdowns.

---

## Quick warning (read this first)

Only use this tool on targets you own or where you have **explicit written authorization**. Running flooding tools against systems without permission is illegal and can cause real damage. Use responsibly.

---

## Features

* Realistic, randomized mobile-style `User-Agent` and headers.
* Random cookies, query parameters, and fake POST/JSON payloads.
* Adaptive thread calculation based on device load (Termux/Android aware).
* Basic rate-limit detection (status and headers).
* Conservative defaults and caps for safer mobile use.
* Interactive terminal UI with a clean banner and prompts.
* Session reuse for better performance and simple stats reporting.
* Minimal external dependencies.

---

## Requirements

* Python 3.8+ (3.10+ recommended)
* ~50 MB free disk space and working network/DNS
* The following Python packages:

```
requests
faker
rich
termcolor
colorama
urllib3
```

Install with:

```bash
pip install -r requirements.txt
```

`requirements.txt` contents:

```
requests
faker
rich
termcolor
colorama
urllib3
```

---

## Install & run

### On Kali Linux

1. Update and install Python if needed:

```bash
sudo apt update && sudo apt install -y python3 python3-pip git
git clone https://github.com/TEAMBCS/D-DoS.git
cd D-DOS
pip3 install -r requirements.txt
python3 ddos-l.py
```

### On Termux (Android)

1. Install / update packages:

```bash
pkg update -y && pkg upgrade -y
pkg install -y python git
git clone https://github.com/TEAMBCS/D-DoS.git
cd D-DOS
pip install -r requirements.txt
python ddos-t.py
```

**Tip for Termux:** if you see SSL or certificate issues, ensure `ca-certificates` is installed: `pkg install ca-certificates`.

---

## How it works (quick)

When you run the script:

1. Prompts for target URL, port, duration, RPS and verbose mode.
2. Validates and normalizes the target URL (DNS resolution check).
3. Measures system load and calculates a conservative thread count.
4. Starts worker sessions that send randomized GET/POST/HEAD requests at the requested RPS.
5. Tracks success, errors, status codes and rate-limit signals.
6. Prints a neat summary at the end.

---

## Usage

### Interactive run (recommended)

```bash
python3 ddos-t.py or ddos-l.py
```

Follow the prompts:

* `Enter Target Url:` e.g. `https://testphp.vulnweb.com/login.php`
* `Enter Port:` e.g. `443` (press Enter for default)
* `Enter Time:` duration in seconds, e.g. `60`
* `Enyer Rps:` requests per second, e.g. `10`
* `USE Verbose (y/n):` `y` or `n`

### Non-interactive one-liner

Pipe answers to run without typing:

```bash
printf "https://testphp.vulnweb.com/login.php\n443\n60\n10\ny\n" | python3 DDOST.py
```

### Stop early

Press `Ctrl+C`. The script handles `SIGINT` and attempts a graceful shutdown.

---

## System use chart (component breakdown)

| Component           | What it does                               | Why it matters                                        |
| ------------------- | ------------------------------------------ | ----------------------------------------------------- |
| URL validation      | Normalizes and resolves the target host    | Avoids malformed targets and catches DNS issues early |
| UA generator        | Builds randomized mobile `User-Agent`s     | Makes traffic look varied and realistic               |
| Header generator    | Random Accept/Referer/X-Forwarded-For etc. | Diversifies requests to mimic many clients            |
| Cookie generator    | Generates random cookie strings            | Adds realism for POST/FORM testing                    |
| Payloads            | Fake form and JSON bodies for POSTs        | Tests server processing of different payload types    |
| Thread calculator   | Decides thread count from RPS and load     | Prevents overloading mobile devices                   |
| Workers / Sessions  | Each worker uses `requests.Session()`      | Keeps TCP connections alive for speed                 |
| Rate-limit detector | Detects 429, Retry-After and limit headers | Lets you know when server is throttling traffic       |
| Logging & stats     | Counts successes/errors/status codes       | Simple post-run analysis and tuning                   |

---

## Example output (short)

```
[*] Starting flood on https://testphp.vulnweb.com/login.php for 60 seconds at 10 RPS
[*] Using 8 threads (Android optimized)
[*] System load: 0.12

Flood Results:
Total Requests Sent: 512
Errors Encountered: 12
Elapsed Time: 60.05 s
Actual RPS: 8.53
Success Rate: 97.7%
Rate Limit Detections: 3

Status 200: 500
Status 404: 10
Status 503: 2
```

---

## Recommended safe defaults

* Use RPS values low enough for the target (e.g., 1–10 for public sites).
* Test short durations first (10–60 s) to observe behavior.
* On mobile/Termux, keep thread count conservative (the script does this automatically).
* Always get written permission.

---

## Troubleshooting

* **Invalid URL / DNS errors** — check the host and your network.
* **High error rate on mobile** — reduce RPS/duration and check network stability.
* **SSL warnings** — the tool disables verification for flood requests; only do this in controlled tests.
* **Missing modules** — reinstall with `pip install -r requirements.txt`.

---

## Contributing

Improvements are welcome. If you publish to GitHub, please:

* Add unit tests for new features.
* Keep any potentially intrusive features opt-in and documented.
* Add a LICENSE file (MIT or Apache 2.0 recommended).

Repo: `https://github.com/ADIRTTA/ADI_DDOS.git`

---

## License & legal

No license file is included by default. If you plan to publish this repository publicly, add a license that fits your goals. This README and the tool are provided for educational and authorized security testing only.
