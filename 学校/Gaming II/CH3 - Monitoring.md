#### MCS
在线监控控制系统（MCS），通过订阅meter和event report监控每个EGM的具体信息，EGM会定期报告当前的meter，当特定事件触发时，EGM会立即发送event report给MCS.

#### Cabinet status
我们可以通过`getCabinetStatus`获取到具体状态

cabinetStatus contains
1. (EGM controlled) egmEnabled
2. (Host controlled) hostEnabled, hostLocked, enableGamePlay, enableMoneyIn 
3. (Door status and lamp) cabinetDoorOpen, logicDoorOpen, auxDoorOpen, serviceLampOn
4. (extension g2sA) generalFault, reelTilt, videoDisplayFault, nvStorageFault, generalMemoryFault


当特定事件发生时，状态会改变，例如`door open`

当门打开时，会将`egmEnabled`设置为`False`，当关闭时则设置回`True`


###### 四种不会影响egmEnabled的事件
1. Service lamp on/off
2. backup battery low
3. EGM restart/power up

#### NoteAcceptor
常见事件:
1. stacker door open
2. stacker remove
3. stacker full
4. stacker jammed and fault

我们可以通过`getNoteAcceptorStatus`获取到具体状态

noteAcceptorStatus contains
1. doorOpen, stackerRemoved
2. stackerNearlyFull, stackerFull 
3. stackerJam, stackerFault, acceptorJam, acceptorFault
4. disconnected, illegalActivity
5. firmwareFault, mechanicalFault, opticalFault, componentFault, nvMemoryFault

其他device也大同小异，因此不一一列举，感兴趣的可以查看![[3monitor.pptx]]


如果`egmEnabled = false`或者`hostEnabled = false`，则设备是`disabled`状态

当处于`disabled`状态时
1. NA 不接收 notes
2. PT 不打印任何 ticket
3. CB 不开启任何游戏并停止所有事务以及禁止任何货币进入。

#### Locking
在当前游戏周期完成后，EGM不得启动任何新游戏，接受任何金钱或分发任何金钱(包括转账和代金券)。

正常情况下可能的Locking：
1. handpay
2. 远端要求locking (set cabinet.egmstate = hostlocked)

主机可以通过`setCabinetLockout`将cabinet上锁

```xml
<cabinet deviceId="1" sessionType="G2S_request" ... >
     <setCabinetLockOut lockOut="true"/> 
</cabinet>
```

```xml
<cabinet deviceId="1" sessionType="G2S_response" ... >
     <cabinetStatus 
          egmEnabled="true"  hostEnabled="true" hostLocked="true" 
          enableGamePlay="true" enableMoneyIn="true"
          egmState="G2S_hostLocked" deviceClass="G2S_cabinet" deviceId="1" … 
     />
</cabinet>
```

#### Events
`eventHandler`作为根标签用于管理EGM中的所有时间，包括:
1. Event discovery(事件发现)
2. Manage event subscription lists(管理事件订阅列表)
3. Manage delivery of events(管理事件交付)
4. Manage collection of associated data(管理相关数据的集合)

每台Host都有其独立