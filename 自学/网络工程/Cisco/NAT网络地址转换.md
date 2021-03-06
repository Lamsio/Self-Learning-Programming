## NAT网络地址转换
用于将私有地址转公有地址

NAT分为三类
1. 静态NAT
2. 动态NAT
3. 端口复用

#### 私有地址空间
A类: 10.0.0.0-10.255.255.255
B类: 172.16.0.0 - 172.31.255.255
C类: 192.168.0.0 - 192.168.255.255

#### 静态NAT
![[Pasted image 20220604131714.png]]

当内网设备需要访问外网时，数据包会经过路由器做静态NAT，此时路由器会得到一个地址映射表内部设备的包将会以外网IP的形式访问外网

但静态NAT并没有解决我们面临的问题，以静态NAT形式，一个私有地址就需要一个公有地址，这显然不合理（我干啥不在本地直接用公有地址呢，你说是吧？）

#### 动态NAT
即在路由器上定义一个公网IP池（池内的公网IP必须是你拥有的），其实本质上和静态区别不大，静态是网络管理员手动为每个内网IP分配一个外网IP，而动态则是交给路由器为每个内网IP分配外网IP

#### 端口复用
前两种都没有解决公网IP紧缺的问题（1内网->1外网），但端口复用策略完美的解决了该问题。包从路由器传到外网前会被打上端口号作为标识，这样一个IP就能最多支持65535个内网设备了
![[Pasted image 20220604133513.png]]

#### 配置
1. 静态NAT转换
2. 动态NAT转换
3. 端口复用

###### 静态NAT
建立静态转换：
`Router(config)#ip nat inside source static [内网IP] [外网IP]`

在与内网连接的接口配置：`Router(config-if)#ip nat inside`
在与外网连接的接口配置：`Router(config-if)#ip nat outside`

查看配置: `Router#show ip nat translations`

![[Pasted image 20220604134138.png]]


###### 动态NAT
定义一个公网IP池: `Router(config)#ip nat pool [name] [起始IP段] [结束IP段]`

定义ACL允许内网地址转换: `Router(config)#access-list [access-list-number] permit [source]`

建立动态转换: `Router(config)#ip nat inside source list [access-list-number] [pool]`

![[Pasted image 20220604135017.png]]

###### PAT转换
定义ACL允许内网地址转换: `Router(config)#access-list [access-list-number] permit [source]`

建立动态转换: `Router(config)#ip nat inside source list [access-list-number] interface [interfaceName] overload`
![[Pasted image 20220604135535.png]]

#### 这和静态、动态路由有何区别？
静态路由和动态路由的配置是为了实现网络间通信，而NAT则是做地址转换的

