
---

## 1. Why Can't We Just Use Pre-Shared Symmetric Keys?

In symmetric cryptography, both parties share the same secret key. This works fine between two people, but breaks down fast when you scale up.

The problem: every pair of users needs their own unique key. The number of keys required grows with the **square** of the number of users:

```
Number of keys = n * (n - 1) / 2     [i.e., O(n²)]
```

To make this concrete:

- The internet has roughly **4,536,248,808** users
- That would require over **10 quadrillion** unique keys (~1 × 10¹⁹)
- This is completely impractical to generate, store, and distribute securely

This is known as the **Key Exchange Problem**, and it's the motivation for asymmetric (public-key) cryptography.

---

## 2. History of Public-Key Cryptography

- **1976:** Diffie and Hellman publish their landmark key exchange algorithm — the first public solution to the key exchange problem
- **1977:** RSA algorithm discovered by Rivest, Shamir, and Adleman at MIT — the first practical public-key encryption scheme

There's an interesting historical footnote though:

- Ellis, Cocks, and Williamson at **GCHQ** (UK intelligence) actually discovered both of these concepts in **1973**
- Their work was classified as top secret and not publicly admitted until **1997**

---

## 3. Asymmetric (Public-Key) Cryptography

### The Core Idea

Instead of one shared secret key, each user has a **key pair**:

- A **public key** — shared openly with everyone
- A **private key** — kept secret by the owner

These keys are mathematically linked: what one key encrypts, only the other can decrypt.

**How encryption works:**

1. Alice wants to send Bob a message
2. She encrypts it using **Bob's public key**
3. Only **Bob's private key** can decrypt it
4. Even Alice cannot decrypt it after sending!

### Example Systems

- **RSA** — The most famous asymmetric system. Developed by Rivest, Shamir, and Adleman (1978). Based on number-theoretic properties of natural numbers (prime factorisation). See Section 5 for details.
- **Elliptic Curve Cryptography (ECC)** — Proposed independently in 1985 by Koblitz and Miller. Uses similar mathematical ideas to RSA but over elliptic curves. Achieves the same security as RSA but with **much smaller key sizes**, making it more efficient.

---

## 4. Principles of Modern Cryptography

Any modern cryptographic algorithm should satisfy these four principles:

1. **Large enough key space** to resist brute-force (exhaustive) search
2. **Resistant to frequency analysis** — an attacker can't guess the key from patterns in ciphertext
3. **Avalanche effect** — a small change in plaintext produces a large, unpredictable change in ciphertext
4. **Kerckhoffs's principle** — security depends only on the secrecy of the _key_, NOT the secrecy of the algorithm itself

---

## 5. RSA Encryption

### 5.1 The Maths You Need to Know First

#### Exponentials

- `3⁵` means 3 multiplied by itself 5 times: 3 × 3 × 3 × 3 × 3 = 243
- Key rule: `nᵃ × nᵇ = n^(a+b)`
- Key rule: `(nᵃ)ᵇ = n^(a×b)`

#### Modular Arithmetic

Think of modular arithmetic like a clock. When you go past the maximum, you wrap around.

- `5 + 3 (mod 12) = 8` _(like 3 hours after 5 o'clock = 8 o'clock)_
- `10 + 5 (mod 12) = 3` _(5 hours after 10 o'clock wraps around to 3 o'clock)_
- `9 + 48 (mod 12) = 9` _(48 hours = exactly 4 days, so back to 9 o'clock)_

Modulus simply means: **divide and take the remainder.**

```
10 mod 3  = 1   (10 / 3 = 3 remainder 1)
15 mod 12 = 3   (15 / 12 = 1 remainder 3)
12 mod 12 = 0   (12 / 12 = 1 remainder 0)
```

#### Greatest Common Divisor (GCD)

GCD(A, B) is the largest number that divides both A and B evenly.

- `GCD(15, 10) = 5`
- `GCD(18, 10) = 2`
- `GCD(21, 10) = 1` → 21 and 10 are **relatively prime** (share no common factors)

#### Euler's Totient Function — φ(N)

φ(N) counts how many numbers between 1 and N−1 share no common factors with N.

- `φ(5) = 4` _(numbers 1, 2, 3, 4 — all relatively prime to 5)_
- `φ(6) = 2` _(only 1 and 5 are relatively prime to 6)_
- `φ(7) = 6` _(1, 2, 3, 4, 5, 6 — because 7 is prime)_
- For any **prime** N: `φ(N) = N − 1`
- For a **product of two primes** P and Q: `φ(P×Q) = (P−1) × (Q−1)`

> **Example:** φ(15) = φ(3×5) = (3−1)×(5−1) = 2×4 = **8**. The 8 numbers are: 1, 2, 4, 7, 8, 11, 13, 14.

#### Euler's Totient Theorem

If GCD(M, N) = 1 and M < N, then:

```
M^φ(N) ≡ 1  (mod N)
```

> **Example:** M=5, N=6. φ(6)=(2−1)×(3−1)=2. So 5² = 25 ≡ 1 (mod 6). Check: 25 ÷ 6 = 4 remainder **1**. ✓

An important extension: if `e × d = 1 (mod φ(N))`, then:

```
(Mᵉ)ᵈ ≡ M  (mod N)
```

**This is the mathematical heart of RSA.**

---

### 5.2 RSA Key Generation — Step by Step

|Step|What you do|
|---|---|
|**1**|Choose two large prime numbers **p** and **q**. Calculate `n = p × q`.|
|**2**|Calculate `φ(n) = (p−1) × (q−1)`. Choose **e** and compute **d** such that `e × d = 1 mod φ(n)`.|
|**3**|**Publish** n and e (your public key). **Keep d secret** (your private key). Destroy p and q.|
|**4 — Encrypt**|`c = mᵉ (mod n)` where m is plaintext, c is ciphertext|
|**5 — Decrypt**|`m = cᵈ (mod n)` where d is the private key|

- **Public key** = (e, n)
- **Private key** = (d, n)
- d is the _multiplicative inverse_ of e, calculated using the extended Euclidean algorithm

---

### 5.3 Worked Example: Encrypting 'GAGA'

Using `e = 131`, `n = 323`, `d = 11` _(d is the receiver's secret)_

First, convert letters to ASCII: **G = 71, A = 65**

**Encryption:**

```
71^131  (mod 323) = 10     →  G encrypts to 10
65^131  (mod 323) = 126    →  A encrypts to 126
```

So `GAGA` → `10, 126, 10, 126`

**Decryption:**

```
10^11   (mod 323) = 71  →  71 = G  ✓
126^11  (mod 323) = 65  →  65 = A  ✓
```

> **Note:** In practice you'd never use such tiny primes, and you wouldn't encrypt letter by letter. Real RSA uses thousands-of-bits primes and encrypts whole blocks of data at once.

---

## 6. Hash Functions

### What is a Hash Function?

A cryptographic hash function takes any message **m** and produces a fixed-size "fingerprint" called a **hash** or **digest**: `H(m)`.

They are **one-way / trapdoor functions**, meaning:

- Very **fast** to compute `H(m)` given `m`
- Computationally **infeasible to reverse**: given `H(m)`, you can't find `m`
- Hard to find any two messages m and m′ that produce the **same hash** (a "collision")

### Useful Properties

If Alice generates `H(m)` and publishes it:

1. Anyone who has `m` can **verify** the hash themselves
2. Anyone who _doesn't_ have `m` **cannot figure out** `m` from `H(m)` alone
3. Alice **can't later claim** a different message `m′` was used, since `H(m) ≠ H(m′)`
4. Alice can **prove she knew** `m` when creating the hash, since `H(m)` can't be generated without knowing `m`
5. Once `H(m)` is published, **no one can alter `m`** without being detected — the hash values won't match

### Common Hash Algorithms

|Algorithm|Status|
|---|---|
|**SHA-2**|✅ Current standard — secure and widely used|
|**SHA-1**|❌ Broken — collisions have been demonstrated|
|**MD5**|❌ Broken — collision attacks known since 2005|

### The Birthday Paradox

There are two subtly different collision security requirements:

- **Preimage resistance:** Given `H(m)`, it's hard to find any `m′` with `H(m′) = H(m)`
    
    - Like: _"How many people in a room until someone shares YOUR specific birthday?"_
    - Answer: **≥ 253 people**
- **Collision resistance:** It's hard to find ANY two messages with the same hash
    
    - Like: _"How many people until any two share a birthday?"_
    - Answer: only **≥ 23 people**

These are not the same thing! Collision resistance is much harder to achieve — which is why broken MD5 and SHA-1 are still dangerous even if direct preimage attacks are hard.

---

## 7. Digital Signatures

### The Core Idea

Asymmetric cryptography gives us a way to **prove authorship** of a message. If Alice encrypts something with her **private key**, anyone can decrypt it with her **public key** — and since only Alice has her private key, this proves it came from her.

### Signing a Short Message

- Alice "encrypts" message `m` with her private key `sk_a` → produces `E_sk_a(m)`
- Anyone receiving this can decrypt with Alice's public key `pk_a` to recover `m`
- Since only Alice could have produced `E_sk_a(m)`, it proves she sent it

### Signing a Long Message (Practical Approach)

Encrypting a huge message with RSA would be very slow. Instead, we **hash first**:

1. Calculate the hash of the message: `H(m)`
2. Encrypt the hash with Alice's private key: `E_sk(a)(H(m))`
3. Send both the plaintext and the signed digest: `m . E_sk(a)(H(m))`

**To verify, the recipient:**

1. Decrypts the signed digest using Alice's **public key** to get `H(m)`
2. Independently computes `H(m)` from the received plaintext
3. Compares the two hash values — if they match, the signature is valid ✓

> This combination of asymmetric crypto + hash functions is what makes real-world **digital signatures and digital certificates** work.

---

## 8. Summary

|Concept|What it does|
|---|---|
|**Key Exchange Problem**|Symmetric keys don't scale — n users need O(n²) keys|
|**Asymmetric Cryptography**|Solves this with public/private key pairs|
|**RSA**|Public-key system based on difficulty of factoring large numbers|
|**ECC**|Same idea as RSA but with smaller, more efficient keys|
|**Hash Functions (SHA-2)**|One-way fingerprints — fast to compute, impossible to reverse|
|**Digital Signatures**|Asymmetric crypto + hashing = provable, tamper-evident authorship|

These tools together are the foundation for **digital certificates, TLS/HTTPS**, and most modern secure communication.