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

每台Host都有其独立的event handler device (deviceId = hostId)

事件报告标签是`<eventReport>`，其子元素分别是`<deviceList>`和`<meterList>`，前者说明设备的状态改变，后者说明设备的数据改变。

```xml 
<eventHandler deviceId="1" sessionType="G2S_request" ... >

	<eventReport deviceClass="G2S_cabinet" deviceId="1"

	eventCode="G2S_CBE307" eventText="Cabinet Door Open">
		<deviceList>

			<statusInfo deviceClass="G2S_cabinet" deviceId="1">

				<cabinetStatus egmEnabled="false"

				cabinetDoorDateTime="..." ... />

			</statusInfo>

		</deviceList>

		<meterList>

			<meterInfo ...>

				<deviceMeters deviceClass="G2S_cabinet" deviceId="1">

				<simpleMeter meterName="G2S_cabinetDoorOpenCnt"

				meterValue="12"/>

				</deviceMeters>

			</meterInfo>

		</meterList>

	</eventReport>

</eventHandler>
```

`<getSupportEvent>`标签允许主机确定EGM中设备支持的事件

1. deviceClass(for all classes, G2S_all)
2. deviceId(for all device, -1)

EGM会返回`<supportedEvents>`报告结果。

```xml
# HOST 发送给 EGM
<eventHandler deviceId="1" sessionType="G2S_request" ... >

	<getSupportedEvents deviceClass="G2S_cabinet" deviceId="-1" />
</eventHandler>
```

```xml
# EGM 返回给 HOST
<eventHandler deviceId="1" sessionType="G2S_response" .... >

	<supportedEvents>
		<supportedEvent deviceClass="G2S_cabinet" deviceId="1"

		eventCode="G2S_CBE001"

		eventText="EGM Disabled Cabinet"/>

		<supportedEvent … />

		<!-- more events supported by the device -->

	</supportedEvents>

</eventHandler>
```

此外，主机还能使用`<setEventSub>`、`<getEventSub>`以及`<clearEventSub>`分别去设置，获取以及清除事件

```xml
# HOST 发送事件订阅请求给 EGM
<eventHandler deviceId="1" sessionType="G2S_request" ... >

	<setEventSub>

		<eventHostSubscription

		deviceClass="G2S_cabinet" deviceId="-1" eventCode="-1"

		sendDeviceStatus="true" sendTransaction="true"

		sendClassMeters="false" sendDeviceMeters="true"

		sendUpdatableMeters="false" eventPersist="false" />
		<eventHostSubscription deviceClass="G2S_noteAcceptor"
		deviceId="-1"

		eventCode="-1" sendDeviceStatus="true" />

	</setEventSub>

</eventHandler>
```

```xml
# EGM 处理后向 HOST 返回请求结果
<eventHandler deviceId="1" sessionType="G2S_response" .... >
	<setEventSubAck/>
</eventHandler>
```

###### Persisted & non-persisted
持久与非持久指的是请求的处理过程的差异，如果设置为`persisted`则类似于TCP的原理，host会一直等待EGM，直至其返回ACK。而非持久则类似于UDP的原理，发送一次后，不管有没有收到都不再追究。

`Persisted`的`<eventHandler>`的`sessionType`是G2S_request，而`non-persisted`则是G2S_notification.


###### eventReport
`<eventReport>`标签有三种子元素，分别是`<deviceList>`,`<transactionList>`以及`<meterList>`

```xml
# 
<eventReport ... transactionId="888">

	<deviceList>

		<statusInfo deviceClass="G2S_noteAcceptor" deviceId="1">

			<noteAcceptorStatus configurationId="..."

			noteValueInEscrow="0"/>

		</statusInfo>

	</deviceList>

	...

</eventReport>
```