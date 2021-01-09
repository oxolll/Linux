# 使用Route連線
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/route.png)
> 使兩台VPC使用靜態路由互相ping
>現在兩台VPC皆使用DHCP獲取ip，所以僅能ping通鄰居

## in R1
```
R1(config)#ip route 192.168.1.0 255.255.255.0 12.0.0.2      //設定R1的路由往192.168.1.x網段經由12.0.0.2
```
## in R2
```
R2(config)#ip route 192.168.2.0 255.255.255.0 12.0.0.1      //設定R2的路由往192.168.2.x網段經由12.0.0.1
```
現在兩邊都可互ping /
VPC(左)
```
VPCS> ping 192.168.1.2

84 bytes from 192.168.1.2 icmp_seq=1 ttl=62 time=2.937 ms
84 bytes from 192.168.1.2 icmp_seq=2 ttl=62 time=1.426 ms
```
VPC(右)
```
VPCS> ping 192.168.2.1

84 bytes from 192.168.2.1 icmp_seq=1 ttl=62 time=2.124 ms
84 bytes from 192.168.2.1 icmp_seq=2 ttl=62 time=0.893 ms
```
## 參考資料
[[筆記]Cisco基本指令-路由](https://david50.pixnet.net/blog/post/45224331-%5B%E7%AD%86%E8%A8%98%5Dcisco%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4-%E8%B7%AF%E7%94%B1)