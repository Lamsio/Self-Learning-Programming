![[Pasted image 20220529144444.png]]
![[Pasted image 20220529144808.png]]
![[Pasted image 20220529144908.png]]
![[Pasted image 20220529145142.png]]
![[Pasted image 20220529151013.png]]
一开始Client需要发送一个报文给目标服务器，以上图为例seq为100.
当服务器收到后，需要作出回应，返回了ack101代表收到了seq为100的请求。
同时将这条信息告知给Client，双方根据自己的seq和ack确立与谁进行通信
![[Pasted image 20220529151543.png]]

#### 窗口机制
有时，每次只发送一条信息属实浪费时间，因此我们可以一次性发送duo
![[Pasted image 20220529151842.png]]