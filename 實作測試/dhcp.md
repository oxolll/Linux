# 使用DHCP獲取ip
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/dhcp.png)
> 新增一台VPC使用DHCP獲取ip

## in R2
```
R2(config)#int e0/1
R2(config-if)#ip addr 192.168.1.1 255.255.255.0     //配置e0/1的ip(192.168.1.1)
R2(config-if)#no shut
R2(config-if)#exit
R2(config)#ip dhcp pool DHCP1       //配置DHCP
R2(dhcp-config)#network 192.168.1.0 /24
R2(dhcp-config)#default-router 192.168.1.1
R2(dhcp-config)#dns-server 8.8.8.8

```
## in VPC
```
VPCS> ip dhcp       //使用DHCP獲取ip
DDORA IP 192.168.1.2/24 GW 192.168.1.1

VPCS> show ip       //顯示ip

NAME        : VPCS[1]
IP/MASK     : 192.168.1.2/24
GATEWAY     : 192.168.1.1
DNS         : 8.8.8.8
DHCP SERVER : 192.168.1.1
DHCP LEASE  : 86393, 86400/43200/75600
MAC         : 00:50:79:66:68:03
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:30000
MTU         : 1500

```
## 檢視連線狀況
```
VPCS> ping 192.168.1.1      

84 bytes from 192.168.1.1 icmp_seq=1 ttl=255 time=0.382 ms
84 bytes from 192.168.1.1 icmp_seq=2 ttl=255 time=0.257 ms
^C
VPCS> ping 12.0.0.2

84 bytes from 12.0.0.2 icmp_seq=1 ttl=255 time=0.266 ms
84 bytes from 12.0.0.2 icmp_seq=2 ttl=255 time=0.284 ms
^C
```
> R2各介面皆可被VPC所ping
```
VPCS> ping 12.0.0.1

12.0.0.1 icmp_seq=1 timeout
^C
VPCS>
```
> R1不可被VPC所ping