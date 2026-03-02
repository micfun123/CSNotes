## Monoalphabetic Cipher

**Add info:**

A monoalphabetic cipher is a substitution cipher in which **each letter of the plaintext is replaced by exactly one letter of the ciphertext**, using a fixed substitution alphabet.

* The same plaintext letter always maps to the same ciphertext letter
* The key is the substitution mapping (the shuffled alphabet)
* Examples include the **Caesar cipher** and simple substitution ciphers

**Security properties:**

* Easy to implement
* Vulnerable to **frequency analysis**, because letter frequencies in the ciphertext resemble those of the plaintext
* Not secure by modern standards

**Add example:**

Plain alphabet:

```
ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

Cipher alphabet (key):

```
QWERTYUIOPASDFGHJKLZXCVBNM
```

Plaintext:

```
HELLO
```

Ciphertext:

```
ITSSG
```

---

## Dictionary Attack

**Add info:**

A dictionary attack is a cryptanalytic attack where the attacker attempts to **decrypt a message or guess a key by systematically trying words from a predefined list (dictionary)**.

* Commonly used against password-based systems
* Exploits human tendency to choose predictable passwords
* Faster than brute-force because it avoids unlikely key values

**Used against:**

* Encrypted password files
* Hashes (especially unsalted hashes)
* Weak symmetric keys derived from passphrases

**Add example:**

If a user’s password is encrypted and the attacker suspects it is a common word, the attacker tries:

```
password
letmein
qwerty
football
admin
```

If encrypting one of these words produces a match, the password is compromised.

---

## Polyalphabetic Cipher

**Add info:**

A polyalphabetic cipher uses **multiple substitution alphabets**, changing the mapping between plaintext and ciphertext throughout the message.

* The substitution depends on a **key**
* The same plaintext letter may encrypt to different ciphertext letters
* Designed to defeat simple frequency analysis

**Common example:**

* **Vigenère cipher**

**Security properties:**

* More secure than monoalphabetic ciphers
* Still vulnerable to statistical attacks with sufficient ciphertext
* Key length is critical to security

**Add example (Vigenère cipher):**

Plaintext:

```
ATTACKATDAWN
```

Key:

```
LEMONLEMONLE
```

Ciphertext:

```
LXFOPVEFRNHR
```

---

## Index of Coincidence

**Add info:**

The Index of Coincidence (IC) is a statistical measure used in cryptanalysis to determine **how likely it is that two randomly selected letters from a text are the same**.

* Helps identify whether a cipher is monoalphabetic or polyalphabetic
* Can be used to estimate the **key length** of a polyalphabetic cipher

**Typical values:**

* Random text: ~0.038
* English plaintext: ~0.066

**Use in attacks:**

* If IC ≈ 0.066 → likely monoalphabetic
* If IC is lower → likely polyalphabetic

---

## Cipher Block Chaining (CBC) – Basic

**Add info:**

Cipher Block Chaining (CBC) is a **mode of operation** for block ciphers that enhances security by chaining blocks together.

**How it works:**

1. Plaintext is divided into fixed-size blocks
2. Each plaintext block is XORed with the previous ciphertext block
3. The result is encrypted using the block cipher
4. The first block uses an **Initialization Vector (IV)**

**Properties:**

* Identical plaintext blocks encrypt to different ciphertext blocks
* Requires a secure, unpredictable IV
* Errors propagate to the next block

**Security considerations:**

* Vulnerable to padding oracle attacks if improperly implemented
* Does not provide integrity or authentication
