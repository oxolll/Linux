# Regular Expression
> Three text processing utilities — awk, grep, sed

## Introduction
-Regular Expression is a sequence of characters that define a search pattern.\
-Usually such patterns are used by string searching algorithms for "find" or "find and replace" operations on strings, or for input validation.

## awk
> A tool divide one pattern to more fields each time.
### Format
`awk 'condition1{action 1} condiction2{action2} ...' filename`  
There is a data => value1 value2 value3 value4
if i want to get the second value, i can use `| awk '{print $2}'`\
`$0` =>  value1 value2 value3 value4\
`$1` => value1\
`$4` => value4\
| variable	|   meaning |
| --------- | ----------------------------------------------------------------------|
|    NF	    |represent the numbers of the patterns' fields|
|    NR	    |represent the number of which row be delt with now by awk|
|   FNR     |like NR in current file, but reset the number when read other file |
|    FS	    |contains the field separator character, default value is " "|
|   ARGC    |number of parameters in command line|
|   ARGV    |name of parameters in command line|
|  ENVIRON  |value of system enviroment variable|
|  FILENAME |contains the name of the current input-file |
|   OFS     |stores the output field separator character, default value is "space"|
|   ORS     |stores the output record separator character, default value is "\n"|
|   RS      |stores the current record separator character,  default value is a "\n"|

example:
> raw data  
```
[root@vm ~]# last -n 10
root     pts/1        192.168.154.1    Tue Jun 23 08:58   still logged in
user     pts/0        :0               Tue Jun 23 08:57   still logged in
user     :0           :0               Tue Jun 23 08:56   still logged in
reboot   system boot  3.10.0-123.el7.x Tue Jun 23 08:55 - 09:40  (00:44)
root     pts/2        192.168.154.1    Mon Jun 22 01:35 - 06:05  (04:29)
root     pts/1        192.168.154.1    Mon Jun 22 01:35 - 06:04  (04:29)
user     pts/0        :0               Mon Jun 22 01:34 - 06:05  (04:30)
user     :0           :0               Mon Jun 22 01:34 - 06:05  (04:31)
reboot   system boot  3.10.0-123.el7.x Mon Jun 22 01:34 - 06:05  (04:31)
root     pts/4        192.168.154.1    Mon Jun 22 01:22 - 01:33  (00:11)
```
================ splitor ================================================

> I want to get the data which data includes roo `(^roo)` and gets number of row `(NR)` ,the username `($1)` and ip address `($3)` ,and add the string "first line!" and "last line!" in head`(BEGIN)` and tail`(END)` spilt by "" `(default value)`. 
```
[root@vm ~]# last -n 10 | awk 'BEGIN {print NR". first line!"}/^roo/{print NR"."$1", ipaddr:"$3}END{print NR".last line!"}'
0.first line!
1.root, ipaddr:192.168.154.1
5.root, ipaddr:192.168.154.1
6.root, ipaddr:192.168.154.1
10.root, ipaddr:192.168.154.1
12.last line!
```
================ splitor ================================================
> Now , i want to use ":"`(-F:)` divide the data which i had get to get the data which only has ip address.
```
[root@vm ~]# last -n 10 | awk 'BEGIN {print NR". first line!"}/^roo/{print NR"."$1", ipaddr:"$3}END{print NR".last line!"}' |awk -F: '{print $2}'

192.168.154.1
192.168.154.1
192.168.154.1
192.168.154.1

```

`-F "what"` mean using what to divide pattern to each field (default value: " ")\


## grep

## sed

## Reference
[鳥哥的 Linux 私房菜 第十一章、正規表示法與文件格式化處理](http://linux.vbird.org/linux_basic/0330regularex.php)\
[Regular expression From Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Regular_expression)\
[Linux中 sed 和 awk的用法詳解](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/392291/)\
[AWK From Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/AWK)