# 🎯 Networking Core Protocols

## 📌 Summary

This module covers the most common application-layer networking protocols used for remote access, file transfers, and email communication.
I learned how each protocol works, what port it uses, and how to interact with them manually using tools like `telnet`, `ftp`, `nslookup`, and `whois`.
These concepts are essential for understanding real-world network behavior, troubleshooting, and analyzing security risks.

---

## 🧠 What I Learned

### ✔ Key Protocols

* **FTP** – File Transfer Protocol
* **SMTP** – Simple Mail Transfer Protocol
* **POP3** – Post Office Protocol v3
* **IMAP** – Internet Message Access Protocol

---

### ✔ Default Ports Overview

| Protocol | Transport Protocol | Default Port |
| -------- | ------------------ | ------------ |
| TELNET   | TCP                | 23           |
| DNS      | UDP / TCP          | 53           |
| HTTP     | TCP                | 80           |
| HTTPS    | TCP                | 443          |
| FTP      | TCP                | 21           |
| SMTP     | TCP                | 25           |
| POP3     | TCP                | 110          |
| IMAP     | TCP                | 143          |

This table helps map each service to its commonly used port, which is fundamental for network troubleshooting and security monitoring.

---

## 🔧 Important Commands

### 🔹 **DNS & Domain Information**

* `nslookup <website>`
  Retrieves the IP address associated with a domain name.

* `whois <website>`
  Displays domain registration information (registrar, owner, creation date, etc.).
  Some information may be hidden due to privacy protection.

---

### 🔹 **FTP (File Transfer Protocol)**

## 📷 FTP Example
![FTP Session](/screenshots/ftp.png)

Connect:

```
ftp <ip-address>
```

Useful commands:

* `ls` — lists available files
* `type ascii` — switches to ASCII transfer mode (for text files)
* `get file.txt` — downloads the specified file

---

### 🔹 **SMTP via Telnet**

## 📷 SMTP Example
![SMTP Session](/screenshots/SMTP.png)

Connect:

```
telnet <ip-address> 25
```

SMTP commands:

* `HELO` / `EHLO` — initiates the SMTP session
* `MAIL FROM:` — sets the sender
* `RCPT TO:` — sets the recipient
* `DATA` — starts writing the email body
* `.` — ends the message body
* `QUIT` — closes the session

---

### 🔹 **POP3 via Telnet**

## 📷 POP3 Example
![POP3 Session](/screenshots/POP3.png)

Connect:

```
telnet <ip-address> 110
```

POP3 commands:

* `USER <username>` — identifies the user
* `PASS <password>` — authenticates the user
* `STAT` — displays number + size of messages
* `LIST` — lists messages
* `RETR <num>` — retrieves a message
* `DELE <num>` — marks a message for deletion
* `QUIT` — applies changes and closes the session

---

### 🔹 **IMAP via Telnet**

Connect:

```
telnet <ip-address> 143
```

IMAP commands:

* `LOGIN <user> <pass>` — authenticates
* `SELECT <mailbox>` — opens a mailbox
* `FETCH <num> BODY[]` — retrieves email content
* `MOVE <id> <mailbox>` — moves an email
* `COPY <id> <mailbox>` — copies an email
* `LOGOUT` — ends the session

