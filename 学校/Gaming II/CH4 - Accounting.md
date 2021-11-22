## Slot reporting
Monitoring & Control system(MCS) 会生成一大堆slot operation，包括:
1. Accounting reports for slot revenues
2. Performance reports for popularity

MCS会从slot machine的meter report处收集财政数据并从事件中计算时间数据。

#### Accounting report
展示所有老虎机的收入数据，通常以日，月，年为单位

例如展示`coin-in`,`coin-out`,`slot win by machine`...总结`slot drop`,`jackpot`等赢钱活动。


#### Performance report
对比老虎机的受欢迎程度，根据利用率和投币率分析老虎机的流行变化趋势。

对比实际与理论业绩，判断EGM是否像PAR表所描述的那样运行?

#### Two ways to calculate slot win
1. Monthly slot win = total wager - total payoff
2. Monthly slot win = monthly increment in coin-in - monthly increment in coin-out.
####  Pay table
![[Pasted image 20211122181319.png]]

这个Pay table展示了不同组合所对应的奖赏。

![[Pasted image 20211122181608.png]]

这张表格说明了各个reel有多少个stop. 从这张图得知总共有20\*20\*20种组合。

#### Pay combo table
![[Pasted image 20211122181744.png]]
这个表格中，额外说明了各组合命中的次数以及所要赔付给顾客的金额。

我们可以用`总赔付/总轮回次数`计算出`RTP`

此外，我们还能将`中奖总次数/所有次数`得到中奖概率(Hit frequency)

#### Actual payback percentage
由于每场游戏的概率都是独立的，因此在同样进行十场游戏后，实际的payback percentage可能是10%也可能是400%，因此，需要在长时间的游戏中，结果才能越发趋近于理论payback percentage。

#### Volatility index
PAR Sheet 通常情况下会提供V.I值，该值代表该游戏的波动值，值越大意味着需要更多的时间才能使实际payback percentage趋近于理论payback percentage。

#### Confidence interval
Confidence interval(可信区间)允许使用者判断游戏的实际Payback%是否正常。

越大的V.I意味着:
1. 短期内波动较大

#### gamePlay
gamePlay也是一个class，因此同样能够进行`setGamePlayState`以及`getGamePlayStatus`操作。

```xml
# host 向 EGM 发送getGamePlayStatus请求
<gamePlay deviceId="1" sessionType="G2S_request" … >

	<getGamePlayStatus />

</gamePlay>
```

```xml
# EGM 向 host 返回所需的数据
<gamePlay deviceId="1" sessionType="G2S_response" … >

	<gamePlayStatus egmEnabled="true" hostEnabled=" true"

	themeId="RBG_JackOrBetter" paytableId="RBG_94"

	generalTilt="false" />

</gamePlay>
```

主机能发送`setActiveDenom`请求去设置游玩的game combo
- 从预设的游戏厂商预设的表单中选取
- 如果gamePlay没有任何active denom则无法开始游戏
- 当EGM处于空闲状态时，它只接受活跃状态下的更改(参见实验室)

###### gamePlay device meters
1. Performance
2. Game Denomination
3. Wager category

Performance:

| Meter names | Description | 
| ---- | ---- | 
| wagerAmt | Total amount wagered | 
| egmPaidGameWonAmt,handPaidGameWonAmt | Base paytable win from game play paid by EGM / handpay. Does not include win from bonuses or progressives. |
| egmPaidProgWonAmt,handPaidProgWonAmt | Progressive win resulting from game play, paid by EGM / handpay. Does not include base paytable win. | 
| wonCnt | Number of primary games won by the player |
| lostCnt | Number of primary games lost by the player | 
| tiedCnt | Number of primary games where there were no credits won or lost |
| failedCnt | Number of primary games where no outcome could be determined as the game failed to complete |
| theoPaybackAmt | Theoretical payback amount. Incremented by the amount wagered times the payback percentage of the wager category played. |
| avgPackbackPct | theoPaybackAmt / wagerAmt |
| secWageredAmt | Amount wagered on secondary games, such as double-up features. |
| secWonAmt | Amount won from secondary games. |

#### Preparing accounting report
- Coin-in = wagerAmt at end - wagerAmt at start
- Coin-out = egmPaidGameWonAmt at end – egmPaidGameWonAmt at start
- Slot win = Coin-in - Coin-out
- Actual P.B% = Coin-out / Coin-in
- Theo P.B% = (TheoPaybackAmt at end - TheoPaybackAmt at start) / Coin-in
- Play count = (won at end - won at start) + (lose at end - lose at start)
- Actual hit freq = (won at end - won at start) / actual play count

## Meters
EGM 需要将所有meter数据保存在永久性存储体中，大多数的meter是累加的(e.g: G2S_logicDoorOpenCnt, G2S_wageredCashableAmt)，少部分的meter，例如credit meter是可增可减的。

G2S将meter分为十组，每个G2S Class可以有1种以上的meter。

#### credit meter
credit meter展示了用户所拥有的三种credit的总和，这三种credit分别是:
1. cashable credit
2. non-cashable credit
3. promotional

使用顺序是: non-cashable -> promotional -> cashable

所有赢得的credit都是cashable credit

#### Meter balancing
![[Pasted image 20211122200454.png]]
#### Glossary
```text
Pay table: 一张表，展示中奖组合以及对应的奖项
Hit frequency: 一个玩家为了赢得奖品而参加的游戏的平均次数
Return to Play(RTP): 平均返还给赌客的总赌注百分比，也被称为theoretical payback percentage。
Actual payback percentage: 实际情况的RTP。
```