#### SDES
Key generation:
1. P10
2. LS-1
3. P8(K1)
4. 2->LS-2
5. P8(K2)

Encryption:
1. IP
2. EP(RIGHT)
3. +Key
4. S-BOX
5. P4
6. +LEFT
7. LEFT RIGHT
8. RIGHT LEFT
9. EP(LEFT)
10. 2->3->4->5->6->7

#### RC4
STEP 1
S = [0,1,2,3,4,5,6,7]
T = [KEY REPEATED]

STEP 2
i = 0
j = (j + S[i] + T[i]) mod 8
swap(S[i], S[j]);

STEP 3
i = i+1 mod 8
j = j + S[i] mod 8
swap(S[i], S[j]);
t = (S[i]+S[j]) mod 8
k = S[t]

#### RSA
n = pq
f(n) = (p-1) x (q-1);
e: 1 <= e <= f(n)
d: e x ? mod n

Pu(e,n)
Pr(d,n)

C = M^e mod n
M' = M^d mod n

#### Elgamal cryptosystem
prime, root, random k, message m, generator g, private key.
1. g^a mod p
2. Y = g^k mod p
3. O = (m(g^a)^k) mod p
4. M' = ((y^-a)O) mod p

#### Elgamal scheme
prime, root, random k, message m, private key Xa

public key: root^Xa mod p
S1: root^k mod p
S2: K^-1(m-XaS1) mod p

V1 = a^m mod p
V2 = Publickey^S1\*S1^S2 mod p

#### S-DES
Key generation:
1. P10
2. LF-1
3. P8
4. LF-2
5. P-8

Encryption
1. IP
2. EP
3. + KEY1
4. S0 S1
5. P4
6. +LEFT
7. + RIGHT
8. EXCHANGE
9. 2-7
10. -IP

#### RC4
STEP 1
S= [0,1,2,3,4,5,6,7]
T = [KEY REPEATED];

STEP 2
i,j = 0
j = (j + S[i]+T[i]) mod 8;
swap(S[i], S[j]);

STEP 3
i,j = 0
i = i+1 mod 8
j = (j + S[i]) mod 8
swap(S[i], S[])