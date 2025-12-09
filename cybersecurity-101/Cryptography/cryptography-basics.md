# 🔐 Cryptography Basics –

## 📄 Key Terms

| Term           | Description                                                                                                                                                             |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Plaintext**  | The original, human-readable data before encryption. It can be a text, image, video, or any binary file.                                                                |
| **Ciphertext** | The scrambled, unreadable output produced after encrypting the plaintext. Ideally, it reveals no information about the original data.                                   |
| **Cipher**     | An algorithm used to convert plaintext to ciphertext and vice versa. Typically developed by cryptographers.                                                             |
| **Key**        | A string of bits used by the cipher to encrypt or decrypt data. While ciphers are public, keys must remain secret (unless using a public key in asymmetric encryption). |
| **Encryption** | The process of converting plaintext into ciphertext using a cipher and a key.                                                                                           |
| **Decryption** | The reverse of encryption — converting ciphertext back to plaintext using the same (or a matching) key.                                                                 |

---

## 🔁 Symmetric Encryption Algorithms

| Algorithm                              | Description                                                                                                   |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **DES** (Data Encryption Standard)     | Standard since 1977, uses a 56-bit key. Broken in under 24 hours by 1999. Now considered insecure.            |
| **3DES** (Triple DES)                  | Applies DES three times. Effective key length ~112 bits. Deprecated in 2019, still present in legacy systems. |
| **AES** (Advanced Encryption Standard) | Adopted in 2001, supports key sizes of 128, 192, or 256 bits. Highly secure and widely used today.            |

---

## ✖️ XOR Operation in Cryptography

**XOR (Exclusive OR)** is a binary operation used in many encryption systems. It works as follows:

| A | B | A ⊕ B |
| - | - | ----- |
| 0 | 0 | 0     |
| 0 | 1 | 1     |
| 1 | 0 | 1     |
| 1 | 1 | 0     |

### 🧠 Key Properties:

* `A ⊕ A = 0`
* `A ⊕ 0 = A`
* XOR is **commutative**: `A ⊕ B = B ⊕ A`
* XOR is **associative**: `(A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)`

### 🔐 XOR for Encryption:

Let `P` = plaintext, `K` = key, and `C` = ciphertext:

* Encryption: `C = P ⊕ K`
* Decryption: `C ⊕ K = P`

Because:
`(P ⊕ K) ⊕ K = P ⊕ (K ⊕ K) = P ⊕ 0 = P`

> ⚠️ XOR encryption is only secure if the key is truly random and as long as the message (as in a **one-time pad**).

---

## ➗ Modulo Operation

**Modulo** (represented by `%` or `mod`) gives the **remainder** of a division.

### 📘 Examples:

| Expression | Result | Explanation    |
| ---------- | ------ | -------------- |
| `25 % 5`   | 0      | 25 = 5 × 5 + 0 |
| `23 % 6`   | 5      | 23 = 3 × 6 + 5 |
| `23 % 7`   | 2      | 23 = 3 × 7 + 2 |

### 🔑 Key Points:

* Result is always between `0` and `n - 1` (if `a % n`, then result ∈ `[0, n-1]`)
* Modulo is **not reversible**:
  `x % 5 = 4` → Possible `x` values include `4, 9, 14, 19, ...` (infinite possibilities)

---

## 🧮 Working with Large Numbers

For cryptographic calculations involving very large integers:

* Use **Python** (`int` type handles big integers automatically)
* Or use **WolframAlpha** for quick online math

Example in Python:

```python
# Compute large modulo
a = 123456789123456789
b = 97
print(a % b)
```

---

## ✅ Summary

| Concept           | Description                                 |
| ----------------- | ------------------------------------------- |
| **Plaintext**     | Original readable message                   |
| **Ciphertext**    | Encrypted, unreadable version               |
| **Cipher**        | Algorithm used for encryption/decryption    |
| **Key**           | Secret value used by cipher                 |
| **XOR Operation** | Binary tool for simple symmetric encryption |
| **Modulo (%)**    | Returns the remainder of a division         |