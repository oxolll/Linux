# Regular Expression
> Three text processing utilities — awk, grep, sed

## Introduction
-Regular Expression is a sequence of characters that define a search pattern.\
-Usually such patterns are used by string searching algorithms for "find" or "find and replace" operations on strings, or for input validation.

## awk
> A tool divide one pattern to more fields each time.
### How to work in awk
![](https://github.com/oxolll/Linux/blob/Linux%E7%B3%BB%E7%B5%B1%E8%87%AA%E5%8B%95%E5%8C%96%E9%81%8B%E7%B6%AD/awk%2C%20grep%2C%20sed/awk%E9%81%8B%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9C%96.png)
### Format
`awk 'condition1{action 1} condiction2{action2} ...' filename`  
-----------------------------
`-F "what"` mean using what to divide pattern to each field (default value: " ")\
`-v variable` you can define variable before command\
`--dump-variables[=file]` output the data of global variables to file, default txt is awkvars.out
example:
```
[root@vm ~]# awk --dump-variables=test.out -v apple=123 'END{print apple}' /etc/passwd
123
```
read file test.out
```
[root@vm ~]# cat test.out
ARGC: 2
ARGIND: 1
     .
     .
     .            
TEXTDOMAIN: "messages"
apple: "123"
```
### Support C Language
You can also use while, do/while, for, break, continue for your command.\
Like C divide each command by `;` .\
example :
> in the action can see the command `count+=1   ;print NR$0;` which use `;` to divide two or more commands
```
[root@vm ~]# awk 'BEGIN{count=0}{count+=1  ;print NR$0;} END{print "user count is ", count}' /etc/passwd
1root:x:0:0:root:/root:/bin/bash
            .
            .
            .
35puppet:x:52:52:Puppet:/var/lib/puppet:/sbin/nologin
user count is  35
```
`print` and `printf` can print the data\
There is a data => value1 value2 value3 value4\
if i want to get the second value, i can use `| awk '{print $2}'`\
`$0` =>  value1 value2 value3 value4\
`$1` => value1\
`$4` => value4

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
|  RLENGTH  |length of string is matched|
|  RSTART   |first location of string is matched|
|  SUBSEP   |stores the subline separator character|

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



## grep

## sed

## Reference
[鳥哥的 Linux 私房菜 第十一章、正規表示法與文件格式化處理](http://linux.vbird.org/linux_basic/0330regularex.php)\
[Regular expression From Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Regular_expression)\
[Linux中 sed 和 awk的用法詳解](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/392291/)\
[AWK From Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/AWK)\
[Awk教學](http://tw.gitbook.net/awk/index.html)