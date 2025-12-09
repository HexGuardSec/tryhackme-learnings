# 📡 Nmap – TCP Scanning Cheatsheet

> A concise guide to essential Nmap options and scanning techniques
> Based on the TryHackMe TCP Scanning module.

---

## 🔍 Target Specification

### 🔢 IP Range and Subnet

| Syntax           | Description                                    |
| ---------------- | ---------------------------------------------- |
| `192.168.0.1-10` | Scan IPs from `.1` to `.10` (range scan)       |
| `192.168.0.1/24` | Scan a full `/24` subnet (from `.1` to `.254`) |

---

## 🎯 Scan Types & Discovery

| Option      | Description                                   |
| ----------- | --------------------------------------------- |
| `-sn`       | Host discovery only (ping scan), no port scan |
| `-sL`       | List scan – shows targets without scanning    |
| `-Pn`       | Treat all hosts as online (skip ping)         |
| `-sS`       | TCP SYN scan (stealth scan, common and fast)  |
| `-sT`       | TCP Connect scan (full 3-way handshake)       |
| `-sU`       | UDP scan                                      |
| `-F`        | Fast scan (top 100 most common ports)         |
| `-p-`       | Scan **all** 65535 ports                      |
| `-p 1-1000` | Scan ports 1 to 1000                          |

---

## 🛠️ Service & OS Detection

| Option | Description                                      |
| ------ | ------------------------------------------------ |
| `-sV`  | Detect service versions on open ports            |
| `-O`   | Operating System detection (requires root)       |
| `-A`   | Aggressive: enables `-O`, `-sV`, traceroute, etc |

---

## 🕒 Timing & Performance

### ⏱ Timing Templates

| Option | Description      | Typical Use       |
| ------ | ---------------- | ----------------- |
| `-T0`  | Paranoid         | IDS evasion       |
| `-T1`  | Sneaky           | Stealth scans     |
| `-T2`  | Polite           | Slow environments |
| `-T3`  | Normal (default) | General purpose   |
| `-T4`  | Aggressive       | Fast scans (LAN)  |
| `-T5`  | Insane           | Max speed, risky  |

### ⏳ Advanced Timing Options

| Option                    | Description             |
| ------------------------- | ----------------------- |
| `--min-parallelism <num>` | Minimum parallel probes |
| `--max-parallelism <num>` | Maximum parallel probes |
| `--min-rate <packets/s>`  | Minimum send rate       |
| `--max-rate <packets/s>`  | Maximum send rate       |
| `--host-timeout <time>`   | Max scan time per host  |

#### 📊 Example: Scan Speed (100 common ports with `-F`)

| Timing | Description | Approx. Duration |
| ------ | ----------- | ---------------- |
| `T0`   | Paranoid    | ~9.8 hours       |
| `T1`   | Sneaky      | ~27 minutes      |
| `T2`   | Polite      | ~40 seconds      |
| `T3`   | Normal      | ~0.15 seconds    |
| `T4`   | Aggressive  | ~0.13 seconds    |

---

## 🖥️ Output Formats

| Option       | Format                    |
| ------------ | ------------------------- |
| `-oN <file>` | Normal text output        |
| `-oX <file>` | XML                       |
| `-oG <file>` | Greppable format          |
| `-oA <base>` | All three formats at once |

---

## 🔊 Verbosity & Debugging

| Option      | Description                            |
| ----------- | -------------------------------------- |
| `-v`, `-vv` | Verbosity (more info during scan)      |
| `-d`, `-d9` | Debug mode (for troubleshooting scans) |

---

## 🧪 Example Commands

```bash
# Fast SYN scan on top 100 ports
nmap -sS -F 10.10.10.10

# Ping scan to find live hosts
nmap -sn 192.168.1.0/24

# OS & version detection
nmap -A 10.10.10.5

# Full port scan
nmap -p- -sV 10.10.10.10

# Save scan output in all formats
nmap -A -oA fullscan 192.168.1.1
```

---

## 📌 Conclusion

Nmap is one of the most powerful tools for network scanning and reconnaissance. Mastering these basic flags will help you quickly perform fast, stealthy, or comprehensive scans during penetration tests or network audits.