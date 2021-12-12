#### Calculation
1. Playfair
2. Vagniere
3. S-DES
4. RC4
5. RSA
6. Elgamal Scheme
7. Elgamal Cryptosystem
8. Diffie-Hellman

#### Knowledge
1. Feistel Example (CH 3)
2. Five mode (CH 4)
3. Stream cipher (CH 5)
4. Euler and Fermat (CH 6)
5. HMAC (CH 9)
6. X.509 (CH 10)

## CH 2
#### Playfair
Plaintext: yuanxiaochen
key: lovechina
![[Pasted image 20211212214217.png]]

#### Vigenere
Plaintext: internettechnologies
Key: sirindhorn

![[Pasted image 20211212214354.png]]

## CH 3
#### Feistel Example
![[Pasted image 20211212215220.png]]

#### DES
Symmetric block cipher
- 56-bit key
- 64-bit input block
- 64-bit output block

![[Pasted image 20211212215455.png]]
![[Pasted image 20211212215551.png]]
![[Pasted image 20211212215701.png]]

Notice: small change in key or plaintext produces large change in ciphertext.

## CH 5
#### Stream cipher
Encrypt one byte at a time by XOR with pseudo-random byte.

Important consideration:
- Encryption sequence should have large period
- Keystream should approximate true random number stream
- Key must withstand brute force attack

Comparison to Block stream
1. Stream cipher easy to implement, and faster
2. Block ciphers can use re-use keys



