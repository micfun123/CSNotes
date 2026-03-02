# Cryptosystem and Transposition Cipher - Complete Notes

## Cryptosystem Definition

A cryptosystem consists of a 5-tuple (E, D, M, K, C) such that:

- **M, K, and C are finite sets**
- **M** is the set of plaintexts
- **K** is the set of keys
- **C** is the set of ciphertexts
- **E** is the encryption algorithm: E : M × K ⇒ C
- **D** is the decryption algorithm: D : C × K ⇒ M

### Key Property

For every key k ∈ K and plaintext m ∈ M: **D(E(m, k), k) = m**

This means decryption reverses encryption when using the same key.

![[Pasted image 20260202120152.png]]


---

## Transposition Cipher

### Overview

- Transposition cipher is amongst the classical ciphers
- Works by **rearranging or moving the plaintext letters** in some logical fashion to produce a ciphertext
- Example: Columnar Transposition
- **Letter frequency** in both plaintext and ciphertext are preserved
- However, the **frequency of digraphs, trigrams, etc. are NOT preserved**

### Columnar Transposition Example

**Plaintext:** ATTACK AT DAWN

**Keyword:** CRYPTO (length 6)

#### Step 1: Arrange plaintext in rows under the keyword

```
C R Y P T O
-----------
A T T A C K
A T D A W N
```

#### Step 2: Number columns based on alphabetical order of keyword

```
2 4 6 3 5 1
-----------
C R Y P T O
A T T A C K
A T D A W N
```

#### Step 3: Read columns in numerical order (1, 2, 3, 4, 5, 6)

- Column 1 (O): K, N
- Column 2 (C): A, A
- Column 3 (P): A, A
- Column 4 (R): T, T
- Column 5 (T): C, W
- Column 6 (Y): T, D

**Ciphertext:** KNAATTCWTD

### Another Example

**Plaintext:** MEET ME AT MIDNIGHT

**Keyword:** KEYS (length 4)

#### Step 1: Remove spaces and arrange

```
K E Y S
-------
M E E T
M E A T
M I D N
I G H T
```

#### Step 2: Number columns alphabetically

```
2 1 4 3
-------
K E Y S
M E E T
M E A T
M I D N
I G H T
```

#### Step 3: Read columns in order (1, 2, 3, 4, 5)

- Column 1 (E): E, E, I, G
- Column 2 (K): M, M, M, I
- Column 3 (S): T, T, N, T
- Column 4 (Y): E, A, D, H

**Ciphertext:** EEIGMMMITTNTEADH

---

## Attack on Transposition Cipher

### Vowel Analysis Attack

**Example Ciphertext:** ASAIRITFNMIMTKLSOIEEM

#### Step 1: Count Total Letters

Total letters in ciphertext: **21 letters**

#### Step 2: Find Possible Dimensions

Factors of 21: 1×21, 3×7, 7×3, 21×1

Practical arrangements:

- **3 columns × 7 rows**
- **7 columns × 3 rows**

#### Step 3: Count Vowels in Ciphertext

Vowels (A, E, I, O, U) in ASAIRITFNMIMTKLSOIEEM:

|Position|Letter|Vowel?|
|---|---|---|
|1|A|✓|
|2|S||
|3|A|✓|
|4|I|✓|
|5|R||
|6|I|✓|
|7|T||
|8|F||
|9|N||
|10|M||
|11|I|✓|
|12|M|✓|
|13|T||
|14|K||
|15|L||
|16|S||
|17|O|✓|
|18|I|✓|
|19|E|✓|
|20|E|✓|
|21|M||

**Vowels found:** A, A, I, I, I, I, O, I, E, E = **10 vowels**

**Percentage:** 10/21 = **47.6%**

##### Expected Vowel Distribution in English

- Normal English text: **38-40% vowels**
- Our ciphertext: **47.6% vowels**

**Conclusion:** The vowel percentage is slightly higher than normal but within reasonable range, confirming this is likely a transposition cipher (not substitution, which would change vowel percentage).

#### Step 4: Test Arrangement 1 (7 columns × 3 rows)

##### Arrange ciphertext in 7×3 grid:

```
Column:  1  2  3  4  5  6  7
Row 1:   A  S  A  I  R  I  T
Row 2:   F  N  M  I  M  T  K
Row 3:   L  S  O  I  E  E  M
```

##### Count vowels per column:

|Column|Letters|Vowels|Count|Percentage|
|---|---|---|---|---|
|1|A, F, L|A|1|33.3%|
|2|S, N, S|-|0|0%|
|3|A, M, O|A, O|2|66.7%|
|4|I, I, I|I, I, I|3|100%|
|5|R, M, E|E|1|33.3%|
|6|I, T, E|I, E|2|66.7%|
|7|T, K, M|-|0|0%|

##### Analysis of Distribution:

- **Column 2:** 0% vowels (very unusual)
- **Column 4:** 100% vowels (all I's - very unusual)
- **Column 7:** 0% vowels (very unusual)
- **Highly uneven distribution** suggests this is **NOT** the correct arrangement

#### Step 5: Test Arrangement 2 (3 columns × 7 rows)

##### Arrange ciphertext in 3×7 grid:

```
Column:  1  2  3
Row 1:   A  S  A
Row 2:   I  R  I
Row 3:   T  F  N
Row 4:   M  I  M
Row 5:   T  K  L
Row 6:   S  O  I
Row 7:   E  E  M
```

##### Count vowels per column:

|Column|Letters|Vowels|Count|Percentage|
|---|---|---|---|---|
|1|A, I, T, M, T, S, E|A, I, E|3|42.9%|
|2|S, R, F, I, K, O, E|I, O, E|3|42.9%|
|3|A, I, N, M, L, I, M|A, I, I|3|42.9%|

##### Analysis of Distribution:

- **Column 1:** 42.9% vowels
- **Column 2:** 42.9% vowels
- **Column 3:** 42.9% vowels
- **Even distribution** - each column has exactly 3 vowels
- **Close to expected 40%** for English text
- This suggests **CORRECT arrangement** ✓

#### Step 6: Statistical Comparison

##### Calculate Standard Deviation of Vowel Percentages:

**For 7×3 arrangement:**

- Percentages: 33.3%, 0%, 66.7%, 100%, 33.3%, 66.7%, 0%
- Mean: 42.9%
- Standard Deviation: σ ≈ 37.8% (VERY HIGH)

**For 3×7 arrangement:**

- Percentages: 42.9%, 42.9%, 42.9%
- Mean: 42.9%
- Standard Deviation: σ = 0% (PERFECT)

#### Step 7: Summary of Vowel Analysis Method

##### Key Differences Between Arrangements:

|Metric|7×3 Arrangement|3×7 Arrangement|
|---|---|---|
|**Vowel Distribution**|Highly uneven|Even|
|**Column 1 vowels**|33.3%|42.9%|
|**Column 2 vowels**|0%|42.9%|
|**Column 3 vowels**|66.7%|42.9%|
|**Column 4 vowels**|100%|N/A|
|**Standard Deviation**|High (~38%)|Low (~0%)|
|**Likely Correct?**|❌ NO|✅ YES|

##### Why Even Distribution Matters:

1. **Natural language** has relatively uniform vowel distribution across text segments
2. **Transposition** preserves this property when columns represent sequential text
3. **Uneven distribution** suggests incorrect column arrangement
4. **Even distribution** (≈40% per column) indicates correct reconstruction

##### Decision Rule:

**Choose the arrangement with:**

1. Vowel percentage closest to 40% per column
2. Lowest standard deviation in vowel distribution
3. No columns with 0% or 100% vowels

**Winner:** 3×7 arrangement ✓

#### Step 8: Read Columns to Decrypt

Reading each column from top to bottom:

**Column 1:** A-I-T-M-T-S-E = **AITMTSE** **Column 2:** S-R-F-I-K-O-E = **SRFIKOE** **Column 3:** A-I-N-M-L-I-M = **AINMLIM**

Combining: **AITMTSE SRFIKOE AINMLIM**

##### Rearranging to find words:

Look for common patterns:

- "TIME" from column 1
- "FIRST" from column 2
- "A", "I", "LAIM" from column 3

After anagramming: **"A FIRST TIME LIKE SIMON"** (possible plaintext)

#### Conclusion on Vowel Analysis

The **vowel analysis method** is effective for determining the correct number of columns in a transposition cipher because:

1. It exploits natural language statistics
2. It's faster than trying all anagrams
3. It narrows down possibilities before detailed cryptanalysis
4. It works even without knowing the exact plaintext

**The 3×7 arrangement is correct** based on even vowel distribution across columns.

---

## Vulnerabilities of Transposition Ciphers

1. **Preserves letter frequency** - vulnerable to frequency analysis combined with pattern recognition
2. **Limited keyspace** - number of possible arrangements is limited by message length
3. **Anagramming attacks** - possible for short messages
4. **Known plaintext attacks** - if part of plaintext is known, entire structure can be revealed
5. **Ciphertext-only attacks** - possible using statistical methods and trial-and-error

---

## Defense Strategies

1. **Double transposition** - apply transposition twice with different keys
2. **Combine with substitution** - create a product cipher
3. **Use irregular columnar transposition** - incomplete final rows
4. **Longer keywords** - increases computational complexity
5. **Modern approach** - transposition is not used alone but as component in block ciphers

---

## Summary

- Transposition ciphers rearrange plaintext without changing the letters themselves
- Columnar transposition is a common classical technique
- **Vowel analysis is a powerful attack method** that uses statistical distribution to identify correct column arrangements
- Attacks exploit the preservation of letter frequencies
- Vulnerability to anagramming and statistical analysis
- Not secure for modern cryptographic applications but important for understanding cipher principles
- **Key insight:** Natural language has uniform vowel distribution (~40%) which helps identify correct decryption arrangements

# Permutation Ciphers

## Overview

A **permutation cipher** is a type of transposition cipher where the positions of the plaintext characters are shifted according to a regular system, so that the ciphertext is a permutation of the plaintext.

### Key Concept

- **Permutation** = rearrangement of elements
- Unlike substitution ciphers (which replace characters), permutation ciphers **move** characters to different positions
- The key is the permutation pattern itself

---

## Mathematical Definition

Given a plaintext message of length **n**, a permutation cipher uses a permutation π of the set {1, 2, 3, ..., n} to rearrange the characters.

**Encryption:**

- For plaintext P = p₁p₂p₃...pₙ
- Ciphertext C = p_{π(1)} p_{π(2)} p_{π(3)} ... p_{π(n)}

**Decryption:**

- Apply the inverse permutation π⁻¹
- Plaintext P = c_{π⁻¹(1)} c_{π⁻¹(2)} c_{π⁻¹(3)} ... c_{π⁻¹(n)}

---

## Types of Permutation Ciphers

### 1. Rail Fence Cipher

The Rail Fence cipher writes the message in a zigzag pattern across multiple "rails" (rows), then reads off the rows sequentially.

#### Example: 3 Rails

**Plaintext:** WEAREDISCOVEREDFLEEATONCE

**Write in zigzag pattern across 3 rails:**

```
Rail 1: W . . . E . . . C . . . R . . . L . . . T . . . E
Rail 2: . E . R . D . S . O . E . E . F . E . A . O . C .
Rail 3: . . A . . . I . . . V . . . D . . . E . . . N . .

Reading horizontally:
Rail 1: W     E     C     R     L     T     E
Rail 2:   E R   D S   O E   E F   E A   O C
Rail 3:     A     I     V     D     E     N
```

**Ciphertext (read row by row):** WECRLTEERDSOEEFEAOCAIVDEN

#### Decryption Process:

1. Know the number of rails (key = 3)
2. Calculate the length of each rail
3. Reconstruct the zigzag pattern
4. Read diagonally to recover plaintext

#### Rail Fence Example: 4 Rails

**Plaintext:** THEQUICKBROWNFOX

```
Rail 1: T . . . . . . B . . . . . . X
Rail 2: . H . . . C . . R . . . F . .
Rail 3: . . E . I . . . . O . N . . .
Rail 4: . . . Q . . K . . . W . . . O

Reading horizontally:
Rail 1: T       B         X
Rail 2:   H   C   R     F
Rail 3:     E I     O N
Rail 4:       Q K     W   O
```

**Ciphertext:** TBXHCRFEIONQKWO

---

### 2. Route Cipher

A route cipher writes the plaintext into a grid and reads it out following a specific route (path).

#### Example: Spiral Route (Clockwise)

**Plaintext:** FLEEATONCEWEAREDISCOVERED (24 letters)

**Write into 4×6 grid (row by row):**

```
F L E E A T
O N C E W E
A R E D I S
C O V E R E
```

**Read in clockwise spiral (outside to inside):**

- Top row (left to right): F L E E A T
- Right column (top to bottom): T E S E
- Bottom row (right to left): E R E V O C
- Left column (bottom to top): A O F
- Inner spiral continues...

**Ciphertext:** FLEEATTESEREEVOCAOF... (depends on exact spiral pattern)

#### Common Route Patterns:

1. **Row by row** (normal columnar)
2. **Column by column**
3. **Spiral** (clockwise/counterclockwise)
4. **Diagonal**
5. **Zigzag**

---

### 3. Columnar Transposition (Fixed Permutation)

Already covered in detail in previous notes, but it's a permutation cipher where:

- Key determines column order
- Permutation is applied to blocks of fixed size

**Example:**

```
Keyword: KEY (becomes permutation 2, 1, 3)
K E Y
-----
2 1 3

Plaintext blocks rearranged according to this permutation
```

---

### 4. Block Permutation Cipher

Divides plaintext into fixed-size blocks and applies the same permutation to each block.

#### Example: Block Size 4

**Permutation:** (1→3, 2→1, 3→4, 4→2)

- Position 1 goes to position 3
- Position 2 goes to position 1
- Position 3 goes to position 4
- Position 4 goes to position 2

**Plaintext:** THISISASECRET (pad to multiple of 4: THISISASECRETXXX)

**Block 1: THIS**

```
Original positions: T(1) H(2) I(3) S(4)
After permutation:  I(1) S(2) T(3) H(4)
Result: ISTH
```

**Block 2: ISAS**

```
Original positions: I(1) S(2) A(3) S(4)
After permutation:  A(1) S(2) I(3) S(4)
Result: ASIS
```

**Block 3: ECRE**

```
Original positions: E(1) C(2) R(3) E(4)
After permutation:  R(1) E(2) E(3) C(4)
Result: REEC
```

**Block 4: TXXX**

```
Original positions: T(1) X(2) X(3) X(4)
After permutation:  X(1) X(2) T(3) X(4)
Result: XXTX
```

**Ciphertext:** ISTHASISREECXXTX

---

## Permutation Representation

### Cycle Notation

A permutation can be written in **cycle notation**:

**Example:** π = (1 3 5)(2 4)

- 1 → 3 → 5 → 1 (cycle)
- 2 → 4 → 2 (cycle)

This means:

- Position 1 goes to position 3
- Position 3 goes to position 5
- Position 5 goes to position 1
- Position 2 goes to position 4
- Position 4 goes to position 2

### Two-Line Notation

```
π = ( 1  2  3  4  5 )
    ( 3  4  5  2  1 )
```

Top row: original positions Bottom row: new positions

---

## Security Analysis

### Keyspace

For a permutation of **n** elements:

- Number of possible permutations = **n!**
- Example: n=10 → 10! = 3,628,800 permutations

However, this is still vulnerable to statistical attacks.

### Vulnerabilities

1. **Frequency Analysis**
    
    - Letter frequencies are preserved
    - Character distribution unchanged
2. **Bigram/Trigram Analysis**
    
    - Some adjacent pairs may remain adjacent
    - Pattern analysis can reveal structure
3. **Known Plaintext Attack**
    
    - If attacker knows part of plaintext, can deduce permutation
4. **Ciphertext-Only Attack**
    
    - For block permutations: if block size is small, can use frequency analysis
    - For rail fence: limited number of rails to try
5. **Pattern Recognition**
    
    - Repeated blocks in plaintext create repeated blocks in ciphertext

---

## Strengths of Permutation Ciphers

1. **Diffusion**
    
    - Spreads plaintext information across ciphertext
    - Changes in one plaintext position affect multiple ciphertext positions
2. **Simple Implementation**
    
    - Easy to implement mechanically or electronically
    - No complex mathematical operations
3. **Reversibility**
    
    - Easy to decrypt with the key
    - Clear inverse operation

---

## Modern Applications

### Block Ciphers

Modern block ciphers use permutation as one component:

- **DES (Data Encryption Standard):** Uses permutation boxes (P-boxes)
- **AES (Advanced Encryption Standard):** Uses ShiftRows operation (permutation)

These combine:

- **Substitution** (S-boxes) for confusion
- **Permutation** (P-boxes) for diffusion

### Permutation Networks

- **Feistel Networks:** Use permutation between rounds
- **Substitution-Permutation Networks (SPN):** Alternate substitution and permutation layers

---

## Breaking Permutation Ciphers

### General Strategy

1. **Identify the type** of permutation cipher
    
    - Rail fence, route, columnar, etc.
2. **Determine parameters**
    
    - Block size
    - Number of rails
    - Grid dimensions
3. **Use statistical analysis**
    
    - Letter frequency
    - Digram/trigram frequency
    - Index of Coincidence
4. **Try likely permutations**
    
    - For small keyspaces, brute force
    - For larger keyspaces, use heuristics

### Example: Breaking Rail Fence

**Given ciphertext:** WECRLTEERDSOEEFEAOCAIVDEN

**Steps:**

1. Count letters: 25 letters
2. Try different numbers of rails (2, 3, 4, 5...)
3. For each rail count, reconstruct the zigzag
4. Check if plaintext makes sense

**Try 3 rails:**

- Rail lengths: 9, 10, 6 (calculated based on zigzag pattern)
- Rail 1: WECRLTE (9 letters)
- Rail 2: ERDSOEEFEAOC (12 letters) ❌ Wrong count

**Recalculate for 3 rails with 25 letters:**

- Rail 1: 9 letters
- Rail 2: 10 letters
- Rail 3: 6 letters

**Reconstruct zigzag pattern and read diagonally:** → **WEAREDISCOVEREDFLEEATONCE** ✓

---

## Combining Permutation with Other Techniques

### Double Transposition

Apply permutation twice with different keys:

1. First permutation with key K₁
2. Second permutation with key K₂

Much stronger than single permutation.

### Product Cipher

Combine substitution and permutation:

1. **Substitution** for confusion (hides plaintext statistics)
2. **Permutation** for diffusion (spreads influence)

This is the basis of modern block ciphers!

---

## Key Takeaways

✓ **Permutation ciphers rearrange characters** rather than replacing them ✓ **Many types exist:** rail fence, route, columnar, block permutation ✓ **Security depends on keyspace** (n! for n positions) ✓ **Vulnerable to statistical analysis** since letter frequencies are preserved ✓ **Essential component of modern cryptography** when combined with substitution ✓ **Provides diffusion** - a critical property in cryptographic systems

---

## Practice Problems

### Problem 1: Rail Fence Cipher

Encrypt "CRYPTOGRAPHY" using 3 rails.

### Problem 2: Block Permutation

Given permutation π = (1→2, 2→4, 3→1, 4→3), encrypt "MATHEMATICS" (block size 4).

### Problem 3: Breaking Permutation

Decrypt "HLOOLELWRD" knowing it's a columnar transposition with 5 columns.

---

## Summary Table

|Cipher Type|Key|Block Size|Keyspace|Security Level|
|---|---|---|---|---|
|Rail Fence|# of rails|Variable|~10|Low|
|Route Cipher|Route pattern|Grid size|~100|Low|
|Columnar|Keyword|Keyword length|m!|Low-Medium|
|Block Permutation|Permutation|Fixed n|n!|Medium|

**Note:** All permutation-only ciphers are considered weak by modern standards and should be combined with substitution for practical security.


**Main sections:**

1. **The Four Core Principles** - explained with real-world examples:
    - Large key space (why AES-128 takes 10²¹ years to crack)
    - Resistant to frequency analysis (how modern ciphers hide patterns)
    - Avalanche effect (1 bit change → 50% output change)
    - Kerckhoff's Principle (why algorithms should be public)
2. **Confusion and Diffusion** - Shannon's concepts explained simply:
    - **Confusion**: Makes key-to-ciphertext relationship complex (uses S-boxes)
    - **Diffusion**: Spreads plaintext influence across ciphertext (uses permutations)
    - How they work together in block ciphers
3. **Practical comparisons** showing why classical ciphers fail and modern ciphers succeed