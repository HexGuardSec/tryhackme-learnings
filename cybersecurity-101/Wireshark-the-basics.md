# 📘 **TryHackMe – Wireshark: The Basics**

## 📌 Summary

This module introduces the fundamentals of Wireshark, a powerful network traffic analysis tool used by system administrators, IT engineers, and security analysts.
You learn how to capture packets, analyze protocols, filter traffic, and understand what happens on the network at a low level.

Wireshark is essential for diagnosing network issues, detecting anomalies, and understanding how devices communicate.

---

## 🧠 **What I Learned**

### ✔️ Packet Capture Basics

* How packet capture works on a network interface
* The difference between:

  * **Live capture** (real-time packets)
  * **Offline capture** (PCAP files)
* How Wireshark displays packets:

  * Packet list (top)
  * Packet details (middle)
  * Packet bytes (bottom)

### ✔️ Common Protocols Observed

* **DNS** (domain resolution)
* **HTTP** (web traffic)
* **TCP/UDP** (transport layer)
* **ARP** (local network resolution)

### ✔️ Filtering Traffic

* Wireshark uses **display filters**, not capture filters.
* Examples of important filters learned:

```
dns
http
tcp
udp
icmp
ip.addr == X.X.X.X
tcp.port == 80
dns.qry.name contains "google"
```

### ✔️ Understanding DNS in Wireshark

I learned to identify:

* DNS queries (type A, AAAA, MX, CNAME…)
* DNS responses
* How domains are resolved step-by-step
* Port used: **53**

### ✔️ Understanding TCP Handshake

Recognizing:

* SYN
* SYN/ACK
* ACK

This helps identify proper or broken connections.

### ✔️ Understanding HTTP

* GET requests
* Status codes (200, 301, 404…)
* Host headers
* Clear-text traffic (when not using HTTPS)

---

## 🔧 **Important Commands / Hotkeys**

```
Ctrl + E           Start/Stop capture
Ctrl + K           Open Capture Options
Ctrl + F           Search
Ctrl + /           Filter bar focus
```

Useful filters:

```
ip.addr == <IP>
tcp.flags.syn == 1
http.request
dns.qry.type == 1
```

---

## 📝 **Notes / Key Takeaways**

* Wireshark is not just for cybersecurity; it’s extremely useful for **IT troubleshooting**, especially for:

  * Slow network issues
  * DNS misconfiguration
  * Packet drops
  * Service communication failures
* You don’t need to master every protocol — knowing **how to filter, search, and read essentials** is already enough for an Internal IT Engineer.
* Wireshark sees **everything** happening on the network interface you choose — very powerful but must be used ethically.

---

## ✅ **Conclusion**

This module built a strong foundation in packet analysis.
Understanding DNS, TCP, and HTTP inside Wireshark will help a lot when diagnosing network issues or analyzing suspicious traffic in real-world environments.