# 🔓 John the Ripper (Jumbo John)

## 🛠️ What Is John the Ripper?

**John the Ripper (John)** is a powerful tool for:

* **Brute force** and **dictionary attacks**
* Cracking **hashes** from various formats
* Recovering passwords from protected archives and SSH keys

The version used here is **Jumbo John**, which includes tools like:

* `zip2john`
* `rar2john`
* `ssh2john`
* `unshadow`

---

## 🧠 How Cracking Works

1. A **hash** is non-reversible.
2. John tries a **dictionary of words** (e.g., `rockyou.txt`) by hashing them using the same algorithm.
3. If a hash matches → the password is recovered.
4. This is called a **dictionary attack**.

---

## 🧰 Installation Overview

| Platform         | Installed?                                                        | Notes |
| ---------------- | ----------------------------------------------------------------- | ----- |
| AttackBox / Kali | ✅ Already installed                                               |       |
| Ubuntu           | ❌ Limited version, use `apt install john` or build Jumbo manually |       |
| Windows          | ❌ Download binaries (64/32-bit) from official site                |       |

---

## 📁 Wordlists

You'll need a **wordlist** like:

📄 `/usr/share/wordlists/rockyou.txt`
(Extract with: `gzip -d rockyou.txt.gz` if needed)

---

## 🧪 Basic Syntax

```bash
john [options] [hashfile]
```

### 🔁 Automatic Mode

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashfile.txt
```

* John detects hash type automatically (can be unreliable)

### 🎯 Format-Specific Cracking

```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hashfile.txt
```

📌 Tip: Use `john --list=formats | grep -i "md5"` to find supported formats.

---

## 🔍 Identifying Hash Types

Use **hash-identifier** or websites like:

* [https://www.onlinehashcrack.com/hash-identification.php](https://www.onlinehashcrack.com/hash-identification.php)

Install and run:

```bash
wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py
python3 hash-id.py
```

---

## 🔓 Cracking Linux Passwords (/etc/shadow)

### 1. Combine `/etc/passwd` and `/etc/shadow`

```bash
unshadow passwd.txt shadow.txt > unshadowed.txt
```

### 2. Crack with John

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
```

---

## 🔐 Cracking Windows NTLM Hashes (NT Hash)

* Found in dumped **SAM** or **NTDS.dit**
* Use tools like **Mimikatz** to dump them
* Format often detected automatically, or specify: `--format=NT`

```bash
john --format=NT --wordlist=rockyou.txt ntlm_hashes.txt
```

---

## 📦 Cracking ZIP Files

### 1. Convert ZIP to Hash

```bash
zip2john file.zip > zip_hash.txt
```

### 2. Crack

```bash
john --wordlist=rockyou.txt zip_hash.txt
```

---

## 📦 Cracking RAR Archives

### 1. Convert RAR to Hash

```bash
rar2john file.rar > rar_hash.txt
```

### 2. Crack

```bash
john --wordlist=rockyou.txt rar_hash.txt
```

---

## 🗝 Cracking SSH Private Keys

### 1. Convert id_rsa Key

```bash
/opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
```

> Kali: `/usr/share/john/ssh2john.py`

### 2. Crack

```bash
john --wordlist=rockyou.txt id_rsa_hash.txt
```

---

## ⚙️ Custom Rules

You can create **dynamic password patterns** with John rules.

### 📁 Location of `john.conf`:

* 🧰 TryHackMe: `/opt/john/john.conf`
* ⚙️ Debian systems: `/etc/john/john.conf`

### 🧾 Example Rule

```ini
[List.Rules:PoloPassword]
cAz"[0-9][!£$%@]"
```

* `c`: Capitalizes first letter
* `Az`: Appends characters
* `"[0-9][!£$%@]"`: Adds number and symbol

### ✅ Use the Rule:

```bash
john --wordlist=rockyou.txt --rules=PoloPassword hashfile.txt
```

---

## 🔁 Extra: Listing Available Formats

```bash
john --list=formats
```

Or search:

```bash
john --list=formats | grep -i "sha"
```

---

## 🎯 Recap: Supported Tools

| Tool         | Purpose                                 |
| ------------ | --------------------------------------- |
| `john`       | Main cracking engine                    |
| `unshadow`   | Combine `/etc/passwd` and `/etc/shadow` |
| `zip2john`   | Extract hash from ZIP                   |
| `rar2john`   | Extract hash from RAR                   |
| `ssh2john`   | Extract hash from SSH private key       |
| `hash-id.py` | Identify hash type                      |