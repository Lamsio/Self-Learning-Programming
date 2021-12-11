## Block Ciphers and the DES
#### Stream cipher
每次以1Bit 或者1byte加密

#### Block cipher
每次以64 / 128 bits 作为一个固定大小的块，进行集体加密，得到的结果的大小也是相同的

#### Reversible and Irreversible Mappings
可逆加密，即可以通过密文解密，明文与密文往往是一对一关系

不可逆加密，即不同的明文有可能得到相同的密文，从而导致不可逆。 


#### Feistel Structure for Block Ciphers
Feistal proposed applying two or more simple ciphers in sequence so final result is stronger than component ciphers.

#### Diffusion and Confusion
```text
Diffusion:
	- Statistical nature of the plaintext is reduced in ciphertext.
	
Confusion:
	- Make the relationship between ciphertext and key as complex as possible.
	
```

#### Using the Feistel structure
```text
Block size: 64/128 bits, larger size leads to more diffusion.

Key size: e.g 128 bits: larger size leads to more confusion.
```

#### Data Encryption Standard(DES)
```text
Symmetric block cipher:
- 56-bit key, 64-bit input block, 64-bit output block

Simplified DES:
- Input(plaintext) block: 8-bits
- Output(ciphertext) block: 8-bits
- Key: 10-bits
- Rounds: 2

Encryption: initial permutation, round function, switch halves.

```

