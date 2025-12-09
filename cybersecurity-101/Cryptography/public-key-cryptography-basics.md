# 🔐 Public Key Cryptography

## 📦 Conceptual Analogy

Imagine needing to send secret instructions to a friend. You can ask your friend for a **lock** that only they can unlock — you place the instructions inside a box and secure it with their lock.

* **Box** = Encrypted Message
* **Lock** = Public Key
* **Key to Open** = Private Key
* **Instructions** = Symmetric Key or Cipher

### 🔄 Applied to Cryptography:

| Analogy Element | Cryptographic Equivalent |
| --------------- | ------------------------ |
| Secret Code     | Symmetric Cipher + Key   |
| Lock            | Public Key               |
| Lock’s Key      | Private Key              |

We use **asymmetric encryption (e.g., RSA)** to securely exchange a symmetric key, then switch to symmetric encryption for fast, secure communication.

---

## 🔐 RSA: Public-Key Encryption

RSA allows secure data transmission over insecure channels. Its security is based on the mathematical difficulty of **factoring large prime numbers**.

### 🧮 RSA Core Math:

* Easy to compute: `p × q = n`
* Hard to reverse: Given `n`, find `p` and `q`

Example:

```
p = 982451653031
q = 169743212279
n = p × q = 166764499494295486767649
```

Factoring `n` to retrieve `p` and `q` is computationally intensive if the primes are large (e.g., 300+ digits each).

---

## 🧪 RSA Numerical Example

1. Bob chooses:

   ```
   p = 157
   q = 199
   n = p × q = 31243
   φ(n) = (p - 1)(q - 1) = 30888
   ```

2. Select:

   ```
   e = 163  (relatively prime to φ(n))
   d = 379  (e × d ≡ 1 mod φ(n))
   ```

3. Keys:

   ```
   Public Key = (n, e) = (31243, 163)
   Private Key = (n, d) = (31243, 379)
   ```

4. Encrypt a message `x = 13`:

   ```
   y = x^e mod n = 13^163 mod 31243 = 16341
   ```

5. Decrypt:

   ```
   x = y^d mod n = 16341^379 mod 31243 = 13
   ```

---

## 🧠 RSA in CTFs

Common RSA variables in Capture The Flag (CTF) challenges:

| Variable | Description      |
| -------- | ---------------- |
| p, q     | Prime numbers    |
| n        | p × q            |
| e        | Public exponent  |
| d        | Private exponent |
| m        | Plaintext        |
| c        | Ciphertext       |

Useful tools:

* [RsaCtfTool](https://github.com/Ganapati/RsaCtfTool)
* [rsatool](https://github.com/ius/rsatool)

---

## 🔁 Diffie-Hellman Key Exchange

Used to establish a **shared secret** over an insecure network, without needing prior secrets or using asymmetric encryption repeatedly.

### 🧪 Simplified Example:

1. **Publicly Agreed**:

   ```
   p = 29 (prime)
   g = 3  (generator)
   ```

2. **Private Keys**:

   ```
   Alice: a = 13
   Bob:   b = 15
   ```

3. **Public Keys**:

   ```
   Alice: A = g^a mod p = 3^13 mod 29 = 19
   Bob:   B = g^b mod p = 3^15 mod 29 = 26
   ```

4. **Exchange & Compute Shared Secret**:

   ```
   Alice computes: B^a mod p = 26^13 mod 29 = 10
   Bob computes:   A^b mod p = 19^15 mod 29 = 10
   Shared Key = 10
   ```

---

## 🧾 Server Authentication with SSH

When connecting via SSH:

```
ssh user@host
```

You might see:

```
The authenticity of host can't be established...
ED25519 key fingerprint is...
Are you sure you want to continue connecting? (yes/no)
```

✅ Answering "yes" stores the server’s public key in your `~/.ssh/known_hosts`
⚠️ If the key changes, you’ll get a warning — this can signal a **Man-in-the-Middle** attack.

---

## 👤 Client Authentication via SSH Keys

Instead of passwords, SSH can use **key-based authentication**:

### Generate SSH Key Pair:

```bash
ssh-keygen -t ed25519
```

* Public Key: `~/.ssh/id_ed25519.pub`
* Private Key: `~/.ssh/id_ed25519`
  ⚠️ Keep this file **private and secure**

### SSH Key Types:

| Type         | Description                         |
| ------------ | ----------------------------------- |
| RSA          | Common default key type             |
| Ed25519      | Fast, modern, and secure            |
| ECDSA        | Elliptic Curve variant of DSA       |
| DSA          | Digital Signature Algorithm (older) |
| -SK variants | Secure hardware key-based           |

---

## 🔐 Private SSH Key Handling

* Use **strong passphrases**
* **Never share** private keys
* Use `chmod 600 ~/.ssh/id_ed25519` to secure file permissions
* Use the key with:

  ```bash
  ssh -i ~/.ssh/id_ed25519 user@host
  ```

---

## 🔓 SSH Backdoors in CTFs

* You can drop your **public key** into:

  ```
  ~/.ssh/authorized_keys
  ```

  to gain persistent access.

* Ideal for **reverse shell upgrades** in CTFs or red teaming.

---

## ✍️ Digital Signatures

* Verify authenticity and integrity of messages or files.
* Created using **private key**, verified with **public key**.
* Common in emails, documents, software, and certificates.
* A signed message can prove authorship (non-repudiation).

---

## 📄 Certificates (HTTPS & Trust)

Used to prove a server’s identity on the web. Example:

```
https://tryhackme.com
```

* Certificate signed by an **intermediate CA**
* Trusted because the chain ends in a **Root CA**, which is trusted by:

  * Your OS
  * Your browser (e.g., Firefox, Chrome)

Use **Let's Encrypt** for free TLS certificates.

---

## 🔑 PGP / GPG Encryption

GPG (GNU Privacy Guard) is an open-source implementation of OpenPGP.

Used for:

* Encrypting emails
* Signing documents
* Secure file encryption

### Generate GPG Keys:

```bash
gpg --full-gen-key
```

Options include:

* RSA
* ECC (Curve25519)
* Set expiration, email, name, comment

> GPG private keys can also be encrypted with a **passphrase**, and are vulnerable if leaked.

---

## 📦 GPG in CTFs

* Often used to **decrypt files** or **verify signatures**
* You may be provided a `.gpg` file or key file in a challenge
* If protected with a passphrase, try:

  ```bash
  gpg2john file.gpg > hash.txt
  john hash.txt
  ```

---

## 🧠 Summary Table

| Concept               | Purpose                                |
| --------------------- | -------------------------------------- |
| RSA                   | Asymmetric encryption                  |
| Public / Private Keys | Keypair for secure communication       |
| Diffie-Hellman        | Secure key exchange                    |
| SSH Key Auth          | Authenticate clients without passwords |
| Digital Signatures    | Verify authenticity & integrity        |
| Certificates          | Prove server identity (e.g., HTTPS)    |
| GPG                   | Encrypt/sign files and emails          |