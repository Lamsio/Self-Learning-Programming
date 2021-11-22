#### Slot reporting
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
#### Glossary
```text
Pay table: 一张表，展示中奖组合以及对应的奖项
Hit frequency: 一个玩家为了赢得奖品而参加的游戏的平均次数
Return to Play(RTP): 平均返还给赌客的总赌注百分比，也被称为theoretical payback percentage。
Actual payback percentage: 实际情况的RTP。
```