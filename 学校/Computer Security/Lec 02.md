## Classical Encryption Techniques

#### Terminology
```text
- Plaintext: 原文
- Ciphertext: 密文
- Encryption: 加密过程
- Decryption: 解密过程
- Key: 加密键，应只有Sender和Receiver知道
- Cipher: 加密手法

· Symmetric encryption: 对称加密
· 
```

#### Attacker
###### Attack methods
1. Brute-force attack: 暴力破解，尝试一切可能性
2. Cryptanalysis: 算法推导，利用算法特性，推导明文或密钥

#### Caesar Cipher
```text
思想: 将字母表移动+/- X 位

明文: Hello
后移两位，得到
密文: jgnnq
```

Attacker仅需测试26次，便能暴力破解。
#### Mono-alphabetic cipher
```text
思想: 每个明文字母都对应一个密文簿上的字母

明文: A B C ... X Y Z
密文: D Z Y ... B K L

```

由于密文簿的字母对应表有26阶乘的可能性，因此难以被破解。

但Attacker可以根据语言习惯去推导字母对应表，虽然耗时，但仍有可能破解！

例如英语中字母E的出现几率很大，可以通过该规律找到密文中出现几率最大的字母。

#### Playfair cipher
```text
1. 将Key按顺序排入5*5的矩阵中，字母不可重复出现，I/J为同一字母
2. 明文分两两一组，如（HELLO -> HE LX LO)，出现同样字母以X区隔
3. 对位，若两字母同行则取右边一位，若两字母同列则取下一位
```

#### Vigen\`ere Cipher
```text
利用一张26*26的字母表去找到对应的密文

明文: ILOVEMIMAXUE
key: AWSL

密文: IHGGEIAXATMP

其中明文字母代表横向坐标，key字母代表纵向坐标。
```