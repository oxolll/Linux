# Routing Information Protocol(RIP)
> 有version1 跟version2 兩種 此篇為version2

## 設定rip
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/rip1.png)

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

