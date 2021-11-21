#### MCS
在线监控控制系统（MCS），通过订阅meter和event report监控每个EGM的具体信息，EGM会定期报告当前的meter，当特定事件触发时，EGM会立即发送event report给MCS.

#### Cabinet status
我们可以通过`getCabinetStatus`获取到具体状态

cabinetStatus contains
1. (EGM controlled) egmEnabled
2. (Host controlled) hostEnabled, hostLocked, enableGamePlay, enableMoneyIn 
3. (Door status and lamp) cabinetDoorOpen, logicDoorOpen, auxDoorOpen, serviceLampOn
4. (extension g2sA) generalFault, reelTilt, videoDisplayFault, nvStorageFault, generalMemoryFault
