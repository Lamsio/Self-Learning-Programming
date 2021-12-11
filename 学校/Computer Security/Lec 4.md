## Block Cipher Operation
#### Electronic code book(ECB)
块传输的一种方式，将明文分割成指定大小的块并且用相同的key进行加密

但如果明文块相同，密文块也会重复。

Each block of x plaintext bits is encoded independently using same key.

#### Cipher Block Chaining(CBC)
![[Pasted image 20211030192918.png]]

在ECB基础上插入IV,每个密码块都依赖前一个密码块

其中IV必须被sender和receiver所知，但attacker不能知道。

IV也必须被保护起来，防止被任何未经授权的人士篡改。

因此，通常情况下，IV在不泄露时，是根本不可能被得知的。

但由于每个数据块的加密都依赖前一个密文，因此加密无法并行。
