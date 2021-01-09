# Routing Information Protocol(RIP)
> 有version1 跟version2 兩種 此篇為version2

## 設定rip
![]()

### in R1
```
R1(config)#router rip
R1(config-router)#version 2
R1(config-router)#network 12.0.0.0      //12.0.0.0這裡要發送rip封包
```
### in R2
```
R2(config)#router rip
R2(config-router)#version 2
R2(config-router)#network 12.0.0.0      //12.0.0.0這裡會發送rip封包
R2(config-router)#network 23.0.0.0      //23.0.0.0這裡會發送rip封包
```
### in R3
```
Router(config-if)#router rip
Router(config-router)#version 2
Router(config-router)#network 23.0.0.0      ///23.0.0.0這裡會發送rip封包
```
設定完成

## Passive Interface
![]()

