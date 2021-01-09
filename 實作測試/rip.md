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
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/rip2.png)
> 實際網路並非每個位置都需要送rip，如果10.0.34.0這個網段不要送的話
> 使用10.0.0.0就會都送到，這時候可以加上passive interface就可以避免

### in R3
```
R3(config)#router rip
R3(config-router)#version 2
R3(config-router)#passive-interface e0/1
R3(config-router)#network 10.0.0.0
```
或者使用
```
R3(config)#router rip
R3(config-router)#version 2
R3(config-router)#passive-interface defualt
R3(config-router)#no passive-interface e0/0
R3(config-router)#network 10.0.0.0
```

# 參考資料
[Jan Ho 的網路世界-Routing Information Protocol(RIP) 路由信息協定](https://www.jannet.hk/zh-Hant/post/routing-information-protocol-rip/)