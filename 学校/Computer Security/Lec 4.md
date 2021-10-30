## Block Cipher Operation
#### Electronic code book(ECB)
块传输的一种方式，将明文分割成指定大小的块并且用相同的key进行加密

但如果明文块相同，密文块也会重复。

#### Cipher Block Chaining(CBC)
![[Pasted image 20211030192918.png]]

在ECB基础上插入IV