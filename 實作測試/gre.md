# Generic Routing Encapsulation (GRE) 通用路由封裝


## hub-to-spoke topology
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/tunnel.png)
>外部(loopback)用 eigrp 內部(e0/0)用 rip
>GRE (ip in ip) 沒有安全性

## ipsec over gre tunnel
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/tunnel2.png)
> 加上ipsec 有較高安全性

## 參考資料
[](https://www.jannet.hk/zh-Hant/post/generic-routing-encapsulation-gre/)\
[](https://www.jannet.hk/zh-Hant/post/internet-protocol-security-ipsec/)