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
