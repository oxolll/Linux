# Enhanced Interior Gateway Routing Protocol(EIGRP) 增強型內部網關路由協定
> 屬於混合型，包含 Distance-Vector 與 Link-State (定時檢查鄰居) 的特性
> 是 cisco 自己的 protocol

## 設定eigrp
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/eigrp.png)

### in R1
```
R1(config-if)#router eigrp 1
R1(config-router)#network 192.168.12.0
R1(config-router)#auto-summary
```
### in R2
```
R2(config-if)#router eigrp 1
R2(config-router)#network 192.168.12.0
R2(config-router)#network 192.168.23.
R2(config-router)#auto-summary
```
### in R3
```
R3(config-if)#router eigrp 1
R3(config-router)#network 192.168.23.0
R3(config-router)#auto-summary
```
### 檢查是否建立完成
#### in R2
```
R2(config-router)#do show ip eigrp nei
EIGRP-IPv4 Neighbors for AS(1)
H   Address                 Interface              Hold Uptime   SRTT   RTO  Q  Seq
                                                   (sec)         (ms)       Cnt Num
1   192.168.23.3            Et0/1                    12 00:00:32    9   100  0  4
0   192.168.12.1            Et0/0                    11 00:00:55 1273  5000  0  4
```
## 名詞簡介
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/eigrp2.png)

## summarization
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/eigrp3.png)
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/eigrp4.png)
## 參考資料
[Jan Ho 的網路世界-Enhanced Interior Gateway Routing Protocol(EIGRP) 增強型內部網關路由協定](https://www.jannet.hk/en/post/enhanced-interior-gateway-routing-protocol-eigrp/)