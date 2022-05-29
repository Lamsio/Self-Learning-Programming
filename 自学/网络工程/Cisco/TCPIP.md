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
有时，每次只发送一条信息属实浪费时间，因此我们可以一次性发送多条信息，在发送信息时需要告知size，如下图，A发送的size为3意味着一次发了三条信息，但B回答的是2，意味着B的缓存只能接收2条，也意味着漏了一条
![[Pasted image 20220529151842.png]]

#### 网络层
![[Pasted image 20220529152312.png]]
![[Pasted image 20220529152427.png]]
![[Pasted image 20220529152459.png]]
![[Pasted image 20220529152616.png]]
当局域网A的用户打算发信息给局域网B的用户时。
MAC地址仅作用于LAN，IP地址则作用于WAN

那么问题来了，主机A和C在局域网A中，那么他俩如何得知对方MAC地址的呢？
每台主机会有一个ARP映射表，包含了主机IP以及MAC地址