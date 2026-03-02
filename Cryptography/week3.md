## AES

Advance Encryption

Used everyday for internet browsing and mobile communications.
A form of substitution-Permutation Network (SPN)

**Confusion** obscures the relationship between the key and ciphertext (via substitution), while **diffusion** spreads plaintext statistics across the ciphertext (via permutation)

Evaluation Criteria

1. Security
	Resistanace to cyptoanalysis


2. Cost
3. wadwa

Excellent accross platform
Good security margin
Well suited to smart cards due to low memory
Operates defend well against attacks on smart cards
Fast key setup
Support expanded key and block sizes
good instruction-level parallelisn 

AES Encription works on greed.

The patten goes throught mulltipel rounds of encipion and this is based on the length of the key. 

for 128 bit key length this leads to 10 rounds of encription. 

for N -1 rounds we have  a mixed colum in the encription cycle. in the final round we leave this step out.


## Feistel Ciphers
Transforms the problem of designing a good block cipher
into two sub-problems
• Design a good Key Expansion/Schedule Algorithm (that
derives fresh key material from the initial key)
• Design a good round function F
• each round repeats a set of simple near identical steps
• key is expanded to generate fresh material for each round


K0, K1, . . . , Kn subround keys for
round 0 . . . n − 1
• We split the plaintext into (L0, R0)
• For each round we compute:
•Li +1 = Ri
• Ri +1 = Li ⊕ F (Ri , Ki )
• The final ciphertext is then
(Ln+1, Rn+1)
• The decryption identical, in reverse
order

Expansion (E-expansion): 32-bit
half-block expanded to 48 bits by
duplicating half of bits
• Key mixing (XOR): result XOR’d with
subkey
• Substitution (S-Box): result is divided
into eight 6-bit pieces, each replaced
with four output bits according to a
lookup table
• Permutation (P-Box): the resultant 32
bits are rearranged according to a
fixed permutation

