# Cryptography Notes: Block Cipher Modes and Stream Ciphers

## Block Cipher Modes of Operation

### Electronic Codebook (ECB)

Electronic Codebook (ECB) is a symmetric block cipher mode where each block of data is encrypted independently using the same key. While simple and fast, it is insecure for most purposes because identical plaintext blocks produce identical ciphertext, leaving patterns in the data. It is primarily used for securing small, random data, such as keys.

**Key Aspects of ECB Mode:**

- **Mechanism:** Plaintext is divided into fixed-size blocks (e.g., 128 bits for AES) and encrypted separately with the same key, without chaining or initialization vectors.
- **Weakness:** The deterministic nature means it fails to hide data patterns, which can leak information (e.g., recognizable patterns in encrypted images).
- **Advantages:** It is highly efficient for parallel processing and is robust against data loss, as corruption in one block does not affect others.
- **Use Cases:** Generally restricted to encrypting single blocks of data or situations where confidentiality of data patterns is not required.

### Cipher Block Chaining (CBC)

Cipher Block Chaining (CBC) improves upon ECB by chaining blocks together. The output of each block is XORed into the next block, creating interdependencies that hide patterns in the plaintext.

**Key Aspects of CBC Mode:**

- **Mechanism:** Before encryption, each block of plaintext is XORed with the previous ciphertext block. The first block is XORed with an Initialization Vector (IV).
- **Security:** By chaining blocks, it hides data patterns, offering better security than Electronic Codebook (ECB) mode.
- **Dependencies:** Encryption is inherently serial because each block depends on the completion of the previous one.
- **Error Propagation:** A single bit error in a ciphertext block will corrupt the corresponding plaintext block and the subsequent plaintext block during decryption.
- **Requirements:** Data must be padded to be a multiple of the block size (e.g., 128 bits for AES).

### Output Feedback (OFB)

Output Feedback (OFB) mode is a block cipher mode of operation that turns a block cipher into a synchronous stream cipher by generating a keystream independent of the plaintext. It encrypts by XORing plaintext with the output of a cipher algorithm, then feeds that output back to the input for the next block.

**Key Features of OFB Mode:**

- **Operation:** The block cipher encrypts an Initialization Vector (IV) or the previous output block to produce a keystream. This keystream is then XORed with the plaintext to generate ciphertext.
- **Error Tolerance:** Because only the keystream (not the ciphertext) is fed back, a bit error in the transmission of a ciphertext block only affects the corresponding plaintext block during decryption, preventing error propagation.
- **No Padding Needed:** As a stream cipher, OFB handles data that is not a multiple of the block size, removing the need for padding.
- **Stream Generation:** The keystream generation is independent of the plaintext, allowing the keystream to be pre-calculated before the data arrives.
- **Use Cases:** Ideal for high-speed, real-time encryption in environments with potential transmission errors, such as satellite communications and radio systems.

### Counter Mode (CTR)

Counter Mode (CTR) transforms a block cipher into a stream cipher by encrypting a counter value and XORing the result with the plaintext. While efficient and parallelizable, it has critical security requirements.

**Key Weaknesses of CTR Mode:**

- **Nonce/Counter Reuse (Catastrophic Failure):** If the same key and nonce (initialization vector + counter) are used to encrypt two different messages, an attacker can XOR the two ciphertexts to recover the XOR of the plaintexts, often leading to full decryption.
- **Lack of Integrity/Authenticity:** CTR mode alone does not provide built-in authentication, making it malleable. An attacker can flip specific bits in the ciphertext, resulting in predictable changes in the decrypted plaintext without detection.
- **Bit-Flipping Attacks:** Because CTR behaves as a stream cipher, an attacker with knowledge of the file format can manipulate targeted data, such as changing a "1" to a "2" in a financial document.

### Galois/Counter Mode (GCM)

Galois/Counter Mode (GCM) is a high-performance, authenticated encryption algorithm that provides both data confidentiality and integrity (authentication) in a single, parallelizable operation. Widely used with AES, GCM uses counter mode for encryption and a Galois field multiplication-based hash (GHASH) for authentication, making it ideal for high-speed networks. It is a standard for AEAD (Authenticated Encryption with Associated Data), often used in TLS and IPsec.

**Key Aspects of GCM:**

- **Authenticated Encryption (AEAD):** Combines encryption and authentication to ensure data cannot be read or modified without detection.
- **High Performance:** The structure allows for parallel processing and pipelining, making it efficient for high-speed (10+ Gbps) hardware implementations.
- **Components:** Uses Counter (CTR) mode for encryption and Galois Field (GF(2^128)) multiplication for computing the authentication tag.
- **Associated Data:** GCM can authenticate data that is not encrypted, such as packet headers in network protocols (AAD - Authenticated Associated Data).
- **Initialization Vector (IV):** GCM requires a unique IV (commonly 96 bits) for every encryption operation with the same key to maintain security.

## Stream Ciphers

Stream ciphers encrypt data one byte or bit at a time, rather than in fixed blocks. They are loosely based on the concept of the one-time pad.

**Key Characteristics:**

- **Operation:** Generate a pseudorandom keystream and XOR it with the plaintext.
- **One-Time Pad:** A theoretically perfect cipher that XORs the message with a truly random key of equal length, providing provable security.
- **Security Limitation:** Stream ciphers use pseudorandom keystreams instead of truly random ones, so they can be vulnerable if not properly designed.

### Types of Stream Ciphers

**Synchronous Stream Ciphers:**

- Pseudorandom digits generated independently of plaintext and ciphertext.
- Both sender and receiver must remain synchronized.

**Self-Synchronizing Stream Ciphers:**

- Will resynchronize after a certain number of bytes following a lost byte.

### Linear Feedback Shift Register (LFSR)

LFSRs are simple hardware-efficient pseudorandom generators, but in their basic form they are relatively easy to cryptanalyze.

**Vulnerabilities:**

- With known plaintext, an attacker can calculate the LFSR state and predict the future keystream.
- If the LFSR structure is unknown, the Berlekamp-Massey algorithm can be used to recover it.

**Famous Uses:**

- DVD Content Scramble System (CSS)
- A5/1 (GSM encryption)

### RC4

RC4 was designed in 1987 by Ron Rivest and kept as a trade secret until its description was posted on the Cypherpunks mailing list in 1994. It is an exceptionally simple and compact stream cipher (pseudorandom number generator).

**Structure:**

RC4 operates in two stages:

1. Key Scheduling Algorithm (KSA)
2. Pseudo-Random Generation Algorithm (PRGA)

#### Key Scheduling Algorithm (KSA)

**Step 1: Initialize State Array**

Initialize an array S with values 0 to 255:

```
for i from 0 to 255
    S[i] := i
endfor
```

**Step 2: Permute Based on Key**

Perform single byte swaps throughout the array based on the key:

```
j := 0
for i from 0 to 255
    j := (j + S[i] + key[i mod keylength]) mod 256
    swap values of S[i] and S[j]
endfor
```

Every byte in the array is swapped at least once.

#### KSA Worked Example

Let's walk through a simplified RC4 example with a state array (S) of size 4 and a key length of 3.

**Given:**

- Key = [1, 2, 3]
- State array size = 4

**Step 1: Initialize**

```
S = [0, 1, 2, 3]
j = 0
```

**Step 2: Key Scheduling**

For each i from 0 to 3:

**i = 0:**

```
j = (0 + S[0] + Key[0]) mod 4
  = (0 + 0 + 1) mod 4 = 1
Swap S[0] and S[1]: S = [1, 0, 2, 3]
```

**i = 1:**

```
j = (1 + S[1] + Key[1]) mod 4
  = (1 + 0 + 2) mod 4 = 3
Swap S[1] and S[3]: S = [1, 3, 2, 0]
```

**i = 2:**

```
j = (3 + S[2] + Key[2]) mod 4
  = (3 + 2 + 3) mod 4 = 0
Swap S[2] and S[0]: S = [2, 3, 1, 0]
```

**i = 3:**

```
j = (0 + S[3] + Key[0]) mod 4
  = (0 + 0 + 1) mod 4 = 1
Swap S[3] and S[1]: S = [2, 0, 1, 3]
```

**Final state array after KSA:**

```
S = [2, 0, 1, 3]
```

#### Pseudo-Random Generation Algorithm (PRGA)

The PRGA generates the keystream used for encryption:

```
i := 0
j := 0
while GeneratingOutput:
    i := (i + 1) mod 256
    j := (j + S[i]) mod 256
    swap values of S[i] and S[j]
    K := S[(S[i] + S[j]) mod 256]
    output K
endwhile
```

Each output byte K is XORed with the corresponding plaintext byte to produce ciphertext.

---

## Summary

**Block Cipher Modes:**

- **ECB:** Simple but insecure; reveals patterns.
- **CBC:** Chains blocks; hides patterns but errors propagate.
- **OFB:** Stream cipher mode; error-resistant.
- **CTR:** Parallelizable but requires unique nonces and lacks authentication.
- **GCM:** Authenticated encryption; combines confidentiality and integrity.

**Stream Ciphers:**

- **Concept:** Encrypt bit-by-bit using pseudorandom keystream.
- **LFSR:** Simple but cryptanalytically weak.
- **RC4:** Compact and widely used, though now considered deprecated for most applications due to discovered vulnerabilities.