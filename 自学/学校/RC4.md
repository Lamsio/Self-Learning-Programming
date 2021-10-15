分三步
1. 初始化
2. 初始化S的排序
3. Stream生成
K = [1 2 3 6]
P = [1 2 2 2]
Ciphertext=??

#### 初始化
S[i] = i*j
T[i] = K[i mod keylen] 

S=[0 1 2 3 4 5 6 7]
T=[1 2 3 6 1 2 3 6]

j=0
for i =0 to 7 do
	j=(j+S[i]+T[i]) mod 8
	swap(S[i],S[j])
end

![[Pasted image 20211011123034.png]]
![[Pasted image 20211011123127.png]]
![[Pasted image 20211011123311.png]]
![[Pasted image 20211011124208.png]]
![[Pasted image 20211011124309.png]]
![[Pasted image 20211011124659.png]]
![[Pasted image 20211015101428.png]]