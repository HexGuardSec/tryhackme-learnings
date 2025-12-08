## 📡 TCPDump Command Reference & Usage Guide

### 🎯 Objective

This guide summarizes the most useful `tcpdump` options and filters for packet capture and basic network traffic analysis.

---

## 🧰 Basic Interface & Setup

Before using `tcpdump`, you need to identify the active network interface.

```bash
ip a s
```

This command lists all available interfaces. You’ll use one (e.g., `eth0`, `ens5`, `wlo1`) with `tcpdump`.

---

## 🎯 Filtering by Hosts & Ports

| Command                         | Description                                    |
| ------------------------------- | ---------------------------------------------- |
| `tcpdump host <IP or HOSTNAME>` | Capture traffic from/to a specific host        |
| `tcpdump src host <IP>`         | Capture only packets **from** a specific host  |
| `tcpdump dst host <IP>`         | Capture only packets **to** a specific host    |
| `tcpdump port <PORT>`           | Capture packets from/to a specific port        |
| `tcpdump src port <PORT>`       | Filter by **source** port                      |
| `tcpdump dst port <PORT>`       | Filter by **destination** port                 |
| `tcpdump <PROTOCOL>`            | Filter by protocol (e.g., `icmp`, `ip`, `ip6`) |

---

## 💡 Example Filters

```bash
# Capture SSH traffic (port 22) on all interfaces
tcpdump -i any tcp port 22

# Capture UDP NTP traffic (port 123) on WiFi interface
tcpdump -i wlo1 udp port 123

# Capture HTTPS traffic to/from example.com, save to file
tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap
```

---

## 🔍 Advanced Filtering

| Command Example              | Description                                         |
| ---------------------------- | --------------------------------------------------- |
| `tcpdump greater <LENGTH>`   | Capture only packets larger than the given size     |
| `tcpdump -i ens5 icmp -n`    | Capture ICMP packets, show IPs instead of hostnames |
| `tcpdump -i ens5 port 53 -n` | Capture DNS traffic (port 53), no DNS resolution    |

---

## 🖥️ Packet Output Display Options

| Flag  | Description                                     |
| ----- | ----------------------------------------------- |
| `-q`  | Quick summary mode — minimal output             |
| `-e`  | Show link-layer (MAC address) headers           |
| `-A`  | Display packet contents in ASCII                |
| `-xx` | Display raw packet data in hexadecimal          |
| `-X`  | Show full packets in both hexadecimal and ASCII |

---

## 🔁 Combined Display Examples

```bash
# Show full HTTP packet details (headers + payload)
tcpdump -i eth0 -A -nn port 80

# Hex and ASCII packet analysis
tcpdump -i eth0 -X port 443
```

---

## 🧪 Summary Table of Options

| Option / Command | Use Case / Description                    |
| ---------------- | ----------------------------------------- |
| `tcpdump -q`     | Quiet output, only basic packet info      |
| `tcpdump -e`     | Include Ethernet/MAC headers              |
| `tcpdump -A`     | ASCII view of packet content (e.g., HTTP) |
| `tcpdump -xx`    | Hexadecimal packet data                   |
| `tcpdump -X`     | Hex + ASCII — full detail mode            |

---

## ✅ Bonus Tips

* You can combine filters (AND, OR) using standard logic:

  ```bash
  tcpdump 'tcp port 22 and host 192.168.1.10'
  ```

* Save captures to `.pcap` file:

  ```bash
  tcpdump -i eth0 -w capture.pcap
  ```

* Read `.pcap` file later:

  ```bash
  tcpdump -r capture.pcap
  ```

---

## 🧠 Useful When…

* Debugging connectivity or application issues
* Monitoring unauthorized outbound connections
* Capturing malicious traffic for analysis
* Practicing packet inspection for security training