#### Basic
###### EGM
全称为Electronic gaming machine，也就是常说的slot machine

###### Host
即Slot information systems, slot management system or simply system

基于网络并负责管理游戏

#### Jackpot system
Tranditional progressive
1. Jackpot triggered by EGM

Server-trigger jackpot
1. Jackpot hit may not relate to game outcome at EGM


#### G2S
相比SAS，G2S更加高效地解决各种各样的问题

GSA主要分为`G2S`、`S2S`以及`Transport`

#### Machine model
machine model由许多硬件所构成，常见的有以下几种。
![[Pasted image 20211121164822.png]]
相同的硬件的`device id`不能是相同的。例如`gamePlay`可以是1和2。

#### Common G2S Classes
Overall control:
1. cabinet : physical housing and overall control

Game play and Progressives:
1. gamePlay: control and monitor of game play
2. progressive: traditional progressive jackpot. Jackpot hit is triggered by the EGM
3. mystery: mystery jackpot. Jackpot hit is triggered by jackpot server
4. bonus: awards determined solely by a bonus host

System services for each connected host
1. communications: monitors and controls communication traffic between the EGM and the host
2. meters: discovery and subscription of meters
3. eventHandler: discovery, subscription and distribution of events

Money movement:
1. noteAcceptor, noteDispenser, coinAcceptor, hopper: currency handling
2. voucher: ticket-in ticket-out. Issue and redeem vouchers
3. handpay: large wins and other payouts that cannot be handled by the EGM

Player tracking
1. idReader: player and employee identification reader devices
2. player: tracks player actions and provides incentives in the form of points

#### Status
当设备的状态发生改变时...

指令格式: [class]Status

```xml
#Cabinet门开了，因此disable
<cabinetStatus egmEnabled = "false" cabinetDoorOpen = "true" … />

#Progressive的奖励制度查询
<progressiveStatus hostEnabled = "true" … >
    <levelStatus levelId="1" progValueAmt="10000000" … />
    <levelStatus levelId="2" progValueAmt="25000000" … />
    <levelStatus levelId="3" progValueAmt="88000000" … />
</progressiveStatus>
```
#### Profiles
配置选项，必须永久保存

指令格式: [class]Profile

```xml
# 限制Credit meter为HKD5000,赢得2000以上时需要handpay
<cabinetProfile currencyId="HKD" machineId= "IPM321" … 
   largeWinLimit="200000000" maxCreditMeter= "500000000”
… />

```

#### Meters
统计各项数据的值，必须永久保存

```xml
# 有23元coin-in 8元的credit meter
<meterInfo …> 
   <deviceMeters deviceClass="G2S_cabinet" deviceId="1">
       <simpleMeter meterName="G2S_wageredCashableAmt" meterValue="2300000"/>
       <simpleMeter meterName="G2S_playerCashableAmt" meterValue="800000"/>          
        ... 
     </deviceMeters>
</meterInfo>

```

#### Transaction Log
事务日志，记录每一笔操作的具体情况。必须永久保存
```xml 
<recallLogList>
    <recallLog gameDateTime="..."  playResult="G2S_gameWon" 
           finalWager="500000" finalWin="1000000" /> 
    <recallLog gameDateTime="..."  playResult="G2S_gameLost" 
           finalWager="200000" finalWin="0" /> 
    …
</recallLogList>
```

#### Message
常见的指令:
1. Get[X]Status
2. [X]Status
3. Set[X]State
4. Get[X]Profile
5. [X]Profile
...

Similar commands to get transaction log.

#### Session type
Three types: `request`、`response` and `notification`

一个`class element`有且仅有一个指令子元素

```xml
# EGM发送keepAlive请求，从device 1到host
<communications deviceId="1" sessionType="G2S_request" ... >
     <keepAlive /> 
</communications>
```

```xml
# host响应一个请求，并返回给device 1
<communications deviceId="1" sessionType="G2S_response" ... >
     <keepAliveAck /> 
</communications>
```