# 🔐 Hashing Basics

## 📚 What Is a Hash Function?

A **hash function**:

* Accepts input of **any size**
* Outputs a **fixed-size** digest (summary)
* Is **deterministic**: same input = same output
* Is **non-reversible**: you can't retrieve the input from the hash
* Should cause **major changes** in output even if a single bit of input changes

### 🧪 Minimal Change, Major Difference

Even a single-bit difference changes the hash significantly:

| File | Hex  | Binary     | MD5       | SHA1      | SHA256    |
| ---- | ---- | ---------- | --------- | --------- | --------- |
| T    | 0x54 | `01010100` | `b9ec...` | `c2c5...` | `e632...` |
| U    | 0x55 | `01010101` | `4c61...` | `b2c7...` | `a255...` |

---

## 🛡 Why Is Hashing Important?

### ✔️ Ensures **Data Integrity**

* Detect tampered or corrupted files

### 🔑 Secures **Password Authentication**

* Stores **hash of password**, not the password itself
* When logging in, the system hashes the submitted password and compares it to the stored hash

---

## ⚠️ What Is a Hash Collision?

A **collision** occurs when:

* **Different inputs produce the same hash output**
* Hash functions are designed to **minimize** collisions

### 📦 Pigeonhole Principle

* More possible inputs than outputs → collisions **are inevitable**
* Good hash functions make **engineered collisions infeasible**

### ❌ Broken Hash Functions

| Algorithm | Status   | Why Insecure                 |
| --------- | -------- | ---------------------------- |
| MD5       | ❌ Broken | Collisions found             |
| SHA-1     | ❌ Broken | "Shattered" collision attack |

> Never use MD5 or SHA-1 for secure password storage or file integrity.

---

## 🔐 Password Storage – Good vs. Bad

### ❌ Insecure Practices

| Case Study | Issue                                                  |
| ---------- | ------------------------------------------------------ |
| RockYou    | Stored passwords in **plaintext** (→ rockyou.txt leak) |
| Adobe      | Used **deprecated encryption** & stored hints          |
| LinkedIn   | Used **SHA-1** without salting                         |

### ✅ Secure Password Storage Workflow

1. Choose secure hash: **Bcrypt**, **Scrypt**, **Argon2**, **PBKDF2**
2. Generate **unique salt** for each user
3. Concatenate: `password + salt`
4. Hash using chosen algorithm
5. Store the **hash + salt**

> Salts do **not** need to be secret.

---

## 🌈 Rainbow Tables

A **rainbow table** is:

* A **precomputed list** of hashes and their matching plaintexts
* Allows attackers to reverse hashes **quickly** (if no salt is used)

| Hash      | Password |
| --------- | -------- |
| e10adc... | 123456   |
| e99a18... | abc123   |

### 🛡 Protection: Salting

Salting ensures:

* Even if two users use the same password → they have **different hashes**
* **Rainbow tables become ineffective**

---

## 🛠 Recognizing and Cracking Hashes

### 🔍 Recognizing Hashes

Use tools like:

* `hashid`
* `hash-identifier`
* Manual checks (length, prefix, context)

> Example: SHA-512 hash starts with `$6$`, Bcrypt with `$2a$` or `$2b$`

### 📁 Linux Password Hashes

Stored in `/etc/shadow`:

```
username:$algorithm$parameters$salt$hash:...
```

| Prefix | Algorithm   |
| ------ | ----------- |
| `$y$`  | yescrypt    |
| `$7$`  | scrypt      |
| `$2b$` | bcrypt      |
| `$6$`  | sha512crypt |
| `$1$`  | md5crypt    |

---

## 🪟 Windows Passwords

Stored in the **SAM database**:

* Uses **NTLM** (MD4-based)
* Extracted using tools like **Mimikatz**

Hash types:

* **LM Hash** (legacy)
* **NT Hash** (modern)

> Be careful: NTLM hashes look like MD5/MD4 — context is crucial.

---

## 🧨 Cracking Password Hashes

### ⚒ Tools

* **Hashcat** (GPU)
* **John the Ripper** (CPU)

> GPU cracking is **much faster**, but VMs often lack GPU passthrough

### 📘 Hashcat Syntax

```bash
hashcat -m <hash_type> -a <attack_mode> <hashfile> <wordlist>
```

| Flag       | Meaning                           |
| ---------- | --------------------------------- |
| `-m`       | Hash type (e.g. `1000` = NTLM)    |
| `-a`       | Attack mode (`0` = dictionary)    |
| `hashfile` | File with hash                    |
| `wordlist` | Password list (e.g., rockyou.txt) |

---

## 🔐 File Integrity

Use hashing to ensure files haven't changed during:

* Downloads
* Transfers
* Archiving

### Example:

```bash
sha256sum downloaded.iso
```

Compare output to official hash from website.

---

## 🔁 Finding Duplicates

If two files have the same hash, they’re identical. Use `md5sum` or `sha256sum` to detect and delete duplicates.

---

## 🧾 HMAC – Keyed Hashing for Authentication

An **HMAC** ensures:

* **Integrity**: Message hasn’t been altered
* **Authenticity**: Sender is who they claim

### 🧮 HMAC Formula

```text
HMAC(K, M) = H((K ⊕ opad) || H((K ⊕ ipad) || M))
```

Where:

* `K`: Secret key
* `M`: Message
* `H`: Hash function
* `opad`, `ipad`: Padding constants

Used in:

* **APIs**
* **JWTs**
* **TLS**

---

## 🧠 Final Takeaways

| Concept          | Summary                                                  |
| ---------------- | -------------------------------------------------------- |
| Hashing          | One-way, fixed-size, irreversible digest                 |
| Password Hashing | Never store passwords directly; always hash with salt    |
| File Integrity   | Hash before and after transfer to verify                 |
| Rainbow Tables   | Defeated with proper salting                             |
| HMAC             | Combines hash + key for integrity/authentication         |
| Cracking         | Use Hashcat (GPU) or John (CPU) with wordlists           |
| Prefixes         | Identify hashing algorithms quickly                      |
| VMs              | GPU cracking is inefficient; use host OS for performance |