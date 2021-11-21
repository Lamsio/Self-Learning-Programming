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
``