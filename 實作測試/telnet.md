# 使用telnet 連線
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/telnet.png)

in R1
```
Router>en
Router#conf t
Router(config)#hostname R1
R1(config)#int e0/0
R1(config-if)#ip addr 12.0.0.1 255.255.255.0
R1(config-if)#no shut
R1(config-if)#conf t
R1(config)#line vty 0 4
R1(config-line)#password 12345
R1(config-line)#transport input telnet

```