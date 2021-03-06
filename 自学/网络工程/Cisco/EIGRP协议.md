## EIGRP协议
该协议运行在Cisco设备上，因此其他品牌如华为路由器可能未必支持该协议

优点：
1. 带宽占用低，触发式更新而并非周期性
2. 多网络层协议（IP、IPX、Appletalk、etc...）
3. 支持VLSM与不连续子网
4. 无环路
5. 快速收敛

两台运行EIGRP协议的路由器会在初次通过相互发送简单报文的形式得知彼此存在并建立邻居关系

![[Pasted image 20220531133814.png]]

首先建立邻居关系表，然后进行路由信息的同步和传输，再更新拓扑表中对于该网络的理解，到达某个目的地所有可能的路由，让然后选取最优解再放入自身路由表中。

#### 报文类型
![[Pasted image 20220531134340.png]]

分为五类：
	- Hello : 用于确认邻居关系的简单报文
	- 更新报文 : 仅在开始时以及后续网路拓扑变更时才会发送更新报文，用于更新关系
	- ACK : 更新报文的接收方需要发送ACK报文给发送方进行确认，如果在规定时间内没发送，发送方会连续重新发送16次更新报文，如仍未收到ACK回复，则默认重新确认关系
	- 查询 : 当某条路由丢失时，向邻居查询相关信息

#### EIGRP的Metric
在RIP中，路由的好坏是根据跳数来决定的。
![[Pasted image 20220531135232.png]]
在上面例子中，RIP一定会选择56K的线路，因为只有1跳，但很明显56K的带宽速度极慢，相比两跳的100M实际效率更低！

EIGRP的metric计算比RIP复杂许多，采用5个标准：
1. 带宽
2. 延迟
3. 接口可靠性
4. 复杂度
5. MTU

###### Metric 计算公式
![[Pasted image 20220531135959.png]]
该式子十分复杂，但在默认情况下其实只是`带宽+延迟`而已。


#### DUAL算法
Diffusing Update Algorithm 用于计算最佳无环路经和备用路径

特点:
- 无环拓扑
- 可立即使用的无环备用路径
- 快速收敛
- 低带宽利用率

###### 名词
- 后继路由器 : 下一跳的路由器
- FD : 可行距离，即起点至终点的距离
- FS : 可行后继路由器, 当后继路由器线路中断时，备用后继路由器
- AD : 通告距离，其他路由器通告给自己到达目的地的距离

![[Pasted image 20220531154307.png]]

当多个路由器的Metric相同时，就能达到负载均衡的效果，路由器会随意选择一个作为下一跳路由器，这被称为**等价负载均衡**

#### 配置
`Router(config)# router eigrp autonomous-system`
autonomous-system参数称为自治系统编号
当我们配置邻居时，确保autonomous-system编号是相同的

Router1
IP : 192.168.12.1 255.255.255.0
Autonomous-system : 100
`network 192.168.12.0`

Router2
IP : 192.168.12.2 255.255.255.0
Autonomous-system : 100
`network 192.168.12.0`

###### 常用指令
```
show ip eigrp neighbors - 显示周围邻居

show ip eigrp topology - 显示拓扑表

show ip route eigrp

show ip protocols

show ip eigrp traffic
```

###### 不等价负载均衡
该功能改变了原有的规则（原本规则是取Metric最优的作为下一跳路由），为了避免负载压力过大，允许设置稍差的Metric路由放入路由表中进行负载均衡。
`Router(router-config)# variance 2`

![[Pasted image 20220531172546.png]]