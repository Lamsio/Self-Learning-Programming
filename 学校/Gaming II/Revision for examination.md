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