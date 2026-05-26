# Cryptography — Key Definitions Summary

---

## Classical Ciphers

### Monoalphabetic Cipher
A substitution cipher where **each plaintext letter is always replaced by the same ciphertext letter**, using a fixed substitution alphabet. The key is the shuffled alphabet mapping. Vulnerable to **frequency analysis** because letter frequencies are preserved.

### Polyalphabetic Cipher
A cipher using **multiple substitution alphabets**, so the same plaintext letter can map to different ciphertext letters depending on its position. The key determines which alphabet is used at each step. Example: **Vigenère cipher**. More resistant to frequency analysis than monoalphabetic ciphers, but still vulnerable to statistical attacks.

### Transposition Cipher
A cipher that **rearranges the positions** of plaintext characters without changing the characters themselves. Letter frequency is preserved; digraph/trigram frequency is not. Example: **Columnar Transposition**. Vulnerable to anagramming and vowel analysis attacks.

### Permutation Cipher
A type of transposition cipher that rearranges characters according to a mathematical permutation π. The key is the permutation pattern. Many variants exist: **Rail Fence**, **Route Cipher**, **Columnar Transposition**, **Block Permutation**. Provides **diffusion** but not confusion.

### Rail Fence Cipher
A permutation cipher that writes plaintext in a **zigzag pattern** across a fixed number of "rails" (rows), then reads off each row in order to produce ciphertext. The key is the number of rails.

---

## Cryptosystem

A formal cryptosystem is a **5-tuple (E, D, M, K, C)** where:
- **M** = set of plaintexts
- **K** = set of keys
- **C** = set of ciphertexts
- **E** : M × K → C — encryption function
- **D** : C × K → M — decryption function

**Key property:** For every key k ∈ K and plaintext m ∈ M: `D(E(m, k), k) = m`

---

## Attacks

### Dictionary Attack
An attack that attempts to decrypt a message or guess a key by **systematically trying words from a predefined list**. Faster than brute-force; exploits predictable/common passwords. Most effective against unsalted hashes and weak passphrases.

### Frequency Analysis
An attack exploiting the fact that letters appear at predictable rates in natural language (~40% vowels in English). Effective against monoalphabetic and transposition ciphers.

### Vowel Analysis
A method used to break transposition ciphers by testing different column arrangements and selecting the one where **each column has ~40% vowels** with the lowest standard deviation — matching natural language distribution.

### Berlekamp-Massey Algorithm
An algorithm that can recover the structure of an unknown LFSR from known output, used to cryptanalyse stream ciphers based on LFSRs.

---

## Statistical Measures

### Index of Coincidence (IC)
The probability that two randomly selected letters from a text are the same.
- Random text: ~0.038
- English plaintext: ~0.066
- IC ≈ 0.066 → likely monoalphabetic; lower IC → likely polyalphabetic.
Used to estimate the key length of polyalphabetic ciphers.

---

## Principles of Modern Cryptography

1. **Large key space** — must resist brute-force (exhaustive) search
2. **Resistant to frequency analysis** — patterns in plaintext must not appear in ciphertext
3. **Avalanche effect** — a small change in plaintext produces a large, unpredictable change in ciphertext
4. **Kerckhoffs's Principle** — security depends only on the secrecy of the **key**, not the algorithm

### Confusion
Obscures the relationship between the key and ciphertext. Achieved via **substitution** (S-boxes).

### Diffusion
Spreads plaintext information across the ciphertext so that changing one bit of plaintext affects many ciphertext bits. Achieved via **permutation** (P-boxes).

---

## Symmetric Block Ciphers

### AES (Advanced Encryption Standard)
A **Substitution-Permutation Network (SPN)** used for everyday internet and mobile communications. Operates on a 4×4 byte grid through multiple rounds (10 rounds for 128-bit key, 12 for 192-bit, 14 for 256-bit). Each round applies: SubBytes (substitution), ShiftRows (permutation), MixColumns, and AddRoundKey. The final round omits MixColumns.

### Feistel Cipher
A structure for block ciphers that splits plaintext into two halves (L, R) and applies multiple rounds of:
- `L_{i+1} = R_i`
- `R_{i+1} = L_i ⊕ F(R_i, K_i)`

Decryption is identical to encryption but with keys in reverse order. **DES** is a Feistel cipher. The round function F involves: **E-expansion** (32→48 bits), **XOR with subkey**, **S-box substitution** (48→32 bits), **P-box permutation**.

---

## Block Cipher Modes of Operation

### ECB (Electronic Codebook)
Each block encrypted **independently** with the same key. Simple and parallelisable but **insecure** — identical plaintext blocks produce identical ciphertext blocks, leaking patterns.

### CBC (Cipher Block Chaining)
Each plaintext block is **XORed with the previous ciphertext block** before encryption; the first block uses an **Initialization Vector (IV)**. Hides patterns but encryption is serial. A 1-bit error corrupts the current and next plaintext block during decryption. Requires padding.

### OFB (Output Feedback)
Turns a block cipher into a **synchronous stream cipher**. The block cipher encrypts the IV/previous output to produce a keystream, which is XORed with plaintext. Keystream is independent of plaintext, so errors do **not** propagate. No padding needed.

### CTR (Counter Mode)
Encrypts a counter value to generate a keystream, then XORs with plaintext. **Fully parallelisable**. Requires a unique nonce per message — reusing the same key+nonce with different plaintexts is **catastrophically insecure**. No built-in authentication.

### GCM (Galois/Counter Mode)
**Authenticated Encryption with Associated Data (AEAD)** — combines CTR mode encryption with a GHASH authentication tag (using Galois Field multiplication). Provides both **confidentiality and integrity**. Highly parallelisable. Standard for TLS and IPsec. Requires a unique IV (96-bit) per encryption.

---

## Stream Ciphers

### Stream Cipher
Encrypts data **one bit or byte at a time** by generating a pseudorandom keystream and XORing it with the plaintext. Based on the concept of the one-time pad.

### One-Time Pad
A theoretically **perfectly secure** cipher that XORs the plaintext with a truly random key of equal length. Provably secure but impractical (key must be as long as the message and used only once).

### Synchronous Stream Cipher
Keystream generated **independently of plaintext and ciphertext**. Sender and receiver must stay synchronised.

### Self-Synchronising Stream Cipher
Resynchronises automatically after a fixed number of bytes following a lost byte.

### LFSR (Linear Feedback Shift Register)
A hardware-efficient pseudorandom generator. Cryptographically weak on its own — with known plaintext an attacker can recover the internal state and predict the keystream. Used in legacy systems (CSS for DVD, A5/1 for GSM).

### RC4
A simple, compact stream cipher (1987, Ron Rivest). Uses a **Key Scheduling Algorithm (KSA)** to initialise a 256-byte state array from the key, then a **Pseudo-Random Generation Algorithm (PRGA)** to produce keystream bytes. Now considered **deprecated** due to discovered vulnerabilities.

---

## Asymmetric (Public-Key) Cryptography

### Key Exchange Problem
Symmetric cryptography requires a unique key per pair of users. For n users this requires **n(n−1)/2 keys** — O(n²) — making it impractical at internet scale.

### Asymmetric Cryptography
Each user holds a **key pair**:
- **Public key** — shared openly
- **Private key** — kept secret

What one key encrypts, only the other can decrypt. Solves the key exchange problem.

### RSA
A public-key system based on the **difficulty of factoring large numbers** (Rivest, Shamir, Adleman — 1977/1978).

**Key generation:**
1. Choose two large primes **p** and **q**; compute `n = p × q`
2. Compute `φ(n) = (p−1)(q−1)`; choose **e** coprime to φ(n); compute **d** as the modular inverse of e: `e × d ≡ 1 (mod φ(n))`
3. **Public key** = (e, n) — publish; **Private key** = (d, n) — keep secret; destroy p and q

**Encryption:** `c = mᵉ mod n`
**Decryption:** `m = cᵈ mod n`

### ECC (Elliptic Curve Cryptography)
Uses the same mathematical ideas as RSA but over **elliptic curves** (proposed 1985, Koblitz and Miller). Achieves equivalent security to RSA with **much smaller key sizes**, making it more efficient.

### Euler's Totient Function — φ(N)
Counts integers from 1 to N−1 that are relatively prime to N.
- For prime N: `φ(N) = N − 1`
- For product of two primes: `φ(p × q) = (p−1)(q−1)`

### Euler's Totient Theorem
If `GCD(M, N) = 1` and `M < N`, then `M^φ(N) ≡ 1 (mod N)`.
Extension used in RSA: if `e × d = 1 (mod φ(N))`, then `(Mᵉ)ᵈ ≡ M (mod N)`.

---

## Hash Functions

### Cryptographic Hash Function
A one-way function `H(m)` that maps any message to a **fixed-size digest (fingerprint)**.

Required properties:
- **Fast to compute** `H(m)` given `m`
- **Preimage resistant** — given `H(m)`, infeasible to find `m`
- **Collision resistant** — infeasible to find two messages `m ≠ m′` where `H(m) = H(m′)`
- **Second preimage resistant** — given `m`, infeasible to find `m′ ≠ m` with `H(m′) = H(m)`

| Algorithm | Status |
|-----------|--------|
| SHA-2 | ✅ Current standard — secure |
| SHA-1 | ❌ Broken — collisions demonstrated |
| MD5   | ❌ Broken — collisions known since 2005 |

### Birthday Paradox
- **Preimage resistance**: how many tries to find a message matching a *specific* hash → ~2ⁿ
- **Collision resistance**: how many tries to find *any* two messages with the same hash → ~2^(n/2)

Collision resistance is **much harder to achieve** — analogous to how only 23 people are needed for *any* two to share a birthday, but 253 for someone to share *your* birthday.

---

## Digital Signatures

### Digital Signature
A mechanism using asymmetric cryptography to **prove authorship and message integrity**:
1. Alice hashes her message: `H(m)`
2. Alice encrypts the hash with her **private key**: `E_sk(H(m))`
3. She sends both the message and the signed hash

**Verification:** Recipient decrypts the signed hash with Alice's **public key**, independently computes `H(m)`, and checks they match. Proves the message was sent by Alice and has not been tampered with.

---

## Mathematical Foundations

### Modular Arithmetic
`a mod n` = remainder when a is divided by n. Arithmetic "wraps around" at n, like a clock.

### GCD (Greatest Common Divisor)
`GCD(A, B)` = the largest integer dividing both A and B evenly. If `GCD(A, B) = 1`, A and B are **relatively prime (coprime)**.

### Multiplicative Inverse (mod n)
d is the multiplicative inverse of e mod n if `e × d ≡ 1 (mod n)`. Computed using the **Extended Euclidean Algorithm**. Used in RSA to derive the private key from the public exponent.
