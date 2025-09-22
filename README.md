# Nikto_basics_command
A comprehensive cheat sheet for the Nikto web server scanner. Features practical commands for penetration testing, security audits, and ethical hacking

# 🚀 The Ultimate Nikto Web Scanner Cheat Sheet

A comprehensive, curated list of Nikto commands for penetration testers, security researchers, and ethical hackers. This guide covers everything from basic scans to advanced evasion and reporting techniques.

> **⚠️ Ethical Use Disclaimer**
> The information in this guide is for educational and authorized security testing purposes only. Using these commands against systems you do not have explicit written permission to test is illegal. Always stay within the law and the bounds of ethical hacking.

---

## 🎯 Targeting & Scoping
*Precisely defining your scan's target and scope.*

| Command                                                    | Purpose                                                              |
| :--------------------------------------------------------- | :------------------------------------------------------------------- |
| `nikto -h <host>`                                          | Scans a single target host or IP address.                            |
| `nikto -h <host>/dir/`                                     | Focuses the scan on a specific directory of a web application.       |
| `nikto -h hosts.txt`                                       | Scans a list of hosts from a given text file.                        |
| `nmap -p80 <network> -oG - \| nikto -h -`                  | Pipes Nmap's output directly to Nikto for automated scanning.        |
| `nikto -h <hostname> -vhost <IP>`                          | Scans a virtual host that is hosted on a server with a different IP. |
| `nikto -p 80,443,8080`                                     | Scans a specific list of ports on the target.                        |
| `nikto -root /app/`                                        | Prepends `/app/` to all requests to scan a non-root application.     |

---

## 📝 Output & Reporting
*Saving and formatting your scan results for analysis.*

| Command                                   | Purpose                                                        |
| :---------------------------------------- | :------------------------------------------------------------- |
| `nikto -o report.txt -F txt`              | Saves the output to a plain text file.                         |
| `nikto -o report.html -F htm`             | Creates a clean, readable HTML report.                         |
| `nikto -o report.xml -F xml`              | Saves in XML format for easy import into other tools.          |
| `nikto -o report.csv -F csv`              | Saves in CSV format, perfect for spreadsheets.                 |
| `nikto -o report -F htm txt xml`          | Saves the output in multiple formats simultaneously.           |
| `nikto -append`                           | Appends the output to an existing report file.                 |
| `nikto -Display V`                        | Displays verbose output for deep debugging.                    |

---

## 🛡️ Evasion & Authentication
*Bypassing security controls and scanning authenticated areas.*

| Command                                                        | Purpose                                                              |
| :------------------------------------------------------------- | :------------------------------------------------------------------- |
| `nikto -id user:pass`                                          | Uses credentials for HTTP Basic Authentication.                      |
| `nikto -id "PHPSESSID=..."`                                     | Passes a cookie to scan authenticated sessions.                      |
| `nikto -H "Header: Value"`                                     | Adds a custom header (e.g., JWT `Authorization` token) to requests.  |
| `nikto -evasion <1-8>`                                         | Uses various IDS evasion techniques (e.g., `1` for URI encoding).    |
| `nikto -useragent "..."`                                       | Spoofs the User-Agent string to mimic a legitimate browser.          |
| `nikto -Pause <seconds>`                                       | Waits a specified number of seconds between each test request.       |
| `nikto -timeout <seconds>`                                     | Sets a timeout for how long to wait for a response.                  |

---

## ⚙️ Tuning & Plugin Control
*Customizing the scan for speed, stealth, and precision.*

| Command                               | Purpose                                                                    |
| :------------------------------------ | :------------------------------------------------------------------------- |
| `nikto -update`                       | **(Crucial)** Updates Nikto's plugins and vulnerability databases.         |
| `nikto -list-plugins`                 | Lists all available plugins for targeted scanning.                         |
| `nikto -T <tuning_code>`              | Runs a specific tuning profile (e.g., `-T 4` for Injection checks).        |
| `nikto -T x<tuning_code>`             | Reverse tuning: runs all checks **except** the specified one.              |
| `nikto -plugins <name;name>`          | Runs only the specified plugins.                                           |
| `nikto -plugins -<name>`              | Excludes a specific plugin from the scan.                                  |
| `nikto -maxtime <time>`               | Sets a maximum duration for the scan (e.g., `1h`, `30m`).                  |
| `nikto -mutate <1-6>`                 | Runs mutation tests to discover extra files or subdomains.                 |

---

## ⭐ Putting It All Together: A Comprehensive Example

This command combines multiple options for a powerful, authenticated scan.

```bash
nikto -h 192.168.1.10/app/ -id "session=..." -T 1245 -evasion 1 -maxtime 1h -o final_report.html -F htm
