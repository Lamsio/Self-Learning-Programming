#### CH3
1. G2S events when in a stacker is replaced
2. Persisted event subscription. How to ensure that MCS will receive event reports when the network suffers temporary outage? CH3: P69-70
3. HW1. Q3

#### G2S events of the stacker
![[Pasted image 20211207143402.png]]

###### Process of removing stacker
1. open the auxiliary door(CBE305)
2. put out the stacker(NAE103)
3. insert a empty stacker into the EGM(NAE104)
4. close the auxiliary door(CBE306)


###### Presisted events
The principle of Presisted and non-presisted just like the relationship between TCP and UDP. For presisted event, if host receives the request, it must respond acknowlage with eventAck after processing the event. if the EGM do not receive any ACK for a long time, it will resend the request untill it gets the ACK.

The session_type of persistent events is "G2S_request", while the session_type of non-persistent events is "G2S_notification".

#### CH4
1. Accounting report p.67-68. Show steps
2. confident interval = RTP +- VI / sqrt(play count)
3. Winner and loser report. P5
4. Which EGMs are outside the confident interval?
5. EOD meter subscription. Limitation. P 103-107
6. Audit meter subscription. Write commands to make subscription and collect meter reports.
7. Meter balance.

###### Preparing accounting reports
1. Coin-in = wagerAmt at end - wagerAmt at start
2. Coin-out = egmPaidGameWonAmt at end - egmPaidGameWonAmt at start
3. Slot win = Coin-in - Coin-out
4. Actual Payback% = Coin-out / Coin-in
5. Theo Payback% = (theoPaybackAmt at end - theoPaybackAmt at start) / Coin-in
6. Play count = (wonCnt at end - wonCnt at start) + (lostCnt at end - lostCnt at start)
7. Autual hit freq = ??

###### Confidence interval
The confidence interval allows us to criticize whether the actual payback% is normal.

###### EOD Subscription
EOD Subscription: EGM reports meter once per day

Use command pair meterInfo / meterInfoAck(host must ack).

The host set the subscription with setMeterSub / meterSubList.
![[Pasted image 20211207164338.png]]

Request meter:
1. meters
2. setMeterSub
3. getDeviceMeters
```xml
<meters deviceId="1" sessionType="G2S_request" … >
     <setMeterSub meterSubType="G2S_onEOD" eodBase="1800000" 
          g2s1:onNoteDrop="true" g2s1:onDoorOpen="true">
           <getDeviceMeters deviceClass="G2S_gamePlay"  deviceId="-1" />
    </setMeterSub>
</meters>
```

Response:
1. meters
2. meterSubList
3. getDeviceMeters
```xml
<meters deviceId="1" sessionType="G2S_response" … >
     <meterSubList meterSubType="G2S_onEOD" eodBase="1800000" 
          g2s1:onNoteDrop="true" g2s1:onDoorOpen="true">
           <getDeviceMeters deviceClass="G2S_gamePlay"  deviceId="1" />
           <getDeviceMeters deviceClass="G2S_gamePlay"  deviceId="2" />
           <getDeviceMeters deviceClass="G2S_gamePlay"  deviceId="3" />
     </meterSubList>
</meters>
```

The EOD meter report must be acknowledged! 

Repeat resending until it receives meterInfoAck.

###### Audit meter subscription
make subscription and collect meter reports.
![[Pasted image 20211207171139.png]]

#### CH5
###### Traditional progressive V.S Mystery progressive
![[Pasted image 20211207180321.png]]

###### The formulas of each parameter in Jackpot calculation
ATV = reset + (wager per game) \* contrib / p
RTP = reset\*p / (wager per game) + contrib

refers to P15

#### CH7
###### The process of voucher redemption
![[Pasted image 20211207184843.png]]

EGMs send a voucher redemption request to the host with redeemVoucher.

Identifies the voucher by attribute validationId.

Host replies with authorizeVoucher to indicate whether the voucher is valid.

If the EGMs can not receive authorizeVoucher within the specified time, it rejects the voucher.

###### Some situations that the voucher redemption failed
1. Voucher already redeemed
2. Voucher expired
3. Voucher doest exist
4. Voucher can not be redeemed at this location
5. Redemption in process at another location.

###### how to protect validation ID to prevent counterfeit tickets?
1. All validation ID is issued by host
2. 