## WAN广域网
前面我们在用cisco模拟器模拟网络时，我们是直接将两台路由器之间进行连线，但实际情况下，假设你北京分公司要和南京分公司互联，根本不可能靠拉一条LAN线去实现

#### 为什么需要WAN？
- 分区或分支机构的员工需要与总部通信并共享数据
- 组织经常需要与其他组织远距离共享信息
- 经常出差的员工需要访问公司内部网络

#### 专线
- 如DDN、POS、E1、以太专线等
- 点到点专有线路（安全高效由ISP提供）
- 支持多种物理介质和物理接口标准
- 稳定可靠，配置简单
- 适合长时间的业务需求，价格很高

#### 电路交换
由SP为企业远程网络节点间通信提供的临时数据传输通道，其操作类型类似于电话拨号技术。
- 常见的如ISDN，ADSL
- 逻辑链接持久有效，按需拨号
- 传输介质主要为电话线，也能是光纤

#### 分组交换（包交换）
- 分组交换设备根据数据帧的二层地址来进行路径的选择
- PVC永久虚电路（在交换开始时就已经建立了路由）
- SVC交换虚电路（根据需要建立）
- 常见业务由x.25、FrameRelay
![[Pasted image 20220605175207.png]]


#### WAN物理层
![[Pasted image 20220605175407.png]]

#### WAN常见封装协议
![[Pasted image 20220605180228.png]]

#### HDLC
![[Pasted image 20220605175632.png]]
传统ISO HDLC只支持单协议环境
而Cisco HDLC支持多协议

#### PPP
![[Pasted image 20220605223159.png]]
PPP是应用在点对点的广域网链路上，也就是数据链路层，所谓数据链路层即俩路由器传输之间的线路上，在RouterA->RouterB之间的线路封装了PPP，在RouterB->RouterC之间也能封装别的，例如HDLC

###### 层次结构
![[Pasted image 20220605223843.png]]