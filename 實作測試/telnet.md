# 使用telnet 連線
![](https://github.com/oxolll/Linux/blob/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%B6%B2%E8%B7%AF/%E5%AF%A6%E4%BD%9C%E6%B8%AC%E8%A9%A6/telnet.png)

> 在R2使用telnet連線至R1，並顯示R1的配置資料

in R1
```
Router>en
Router#conf t
Router(config)#hostname R1
R1(config)#en password 66666  //設定密碼(特權密碼)
R1(config)#int e0/0
R1(config-if)#ip addr 12.0.0.1 255.255.255.0
R1(config-if)#no shut
R1(config-if)#conf t
R1(config)#line vty 0 4     //設定Telnet連線數量 0~4，共5組
R1(config-line)#password 12345      //設定密碼(telnet密碼)
R1(config-line)#transport input telnet  //啟動telnet

```

in R2
```
Router>en
Router#conf t
Router(config)#hostname R2
R2(config)#int e0/0
R2(config-if)#ip addr 12.0.0.2 255.255.255.0
R2(config-if)#no shut
R2(config-if)#^Z
R2#telnet 12.0.0.1      //使用telnet連線到R1(12.0.0.1)
Trying 12.0.0.1 ... Open


User Access Verification

Password:       //輸入telnet密碼(12345)
R1>en
Password:       //輸入特權密碼(66666)
R1#show ip int br       //顯示R1的介面配置
Interface                  IP-Address      OK? Method Status                Protocol
Ethernet0/0                12.0.0.1        YES manual up                    up  
Ethernet0/1                unassigned      YES unset  administratively down down
Ethernet0/2                unassigned      YES unset  administratively down down
Ethernet0/3                unassigned      YES unset  administratively down down

```

## 參考資料
[James LAB-Cisco設定遠端連線(Telnet & SSH)](http://www.james-tw.com/cisco/cisco-she-ding-yuan-duan-lian-xian-telnet-ssh)