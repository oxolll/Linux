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
`--dump-variables[=file]` output the data of global variables to file, default txt is awkvars.out\
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
### Functions
coming soon...
### User Difines Functions 
coming soon...
### Redirect Output File
coming soon...
### Format Output Data
coming soon...


## grep
>  A command-line utility for searching plain-text data sets for lines that match a regular expression.
### How to work in sed
![]()
### Format
`grep [option] [target-string] filename/path`  
-----------------------------
#### Common Options
`-n` display number of raws\
`-c` count the numeber of raws\
`-i` regardless capital letter or lowercase\
`-v` exclude the target string\
`-r` recursive search the target path \
`--include` search target string appoint some condition in file, usually use -r together\
`-A n` display n line after the target sting's raw \
`-B n` display n line before the target sting's raw \
`-C n` display n line after and before the target sting's raw \
`--color=` `never` , `auto`, `always` never means no use color, auto means use auto setting, always means using color
#### Using Regular Expression For Search
You can also use regular expression for your command.\
`^ string` using string in head \
`string $` using string in tail \
`^ string *` using string zero time or more in head \
`^ string \?` using string zero time or one in head \
`^ string \+` using string than zero time in head \
`string1 \| string2` using string1 or string2 \
example :\
raw data
```
[root@vm ~]# cat test.txt
a1
a2
a3
a4
a5
a6
a7
a8
a9
a10
```
`^ string` 
```
[root@vm ~]# grep "^1" test.txt
[root@vm ~]# grep "^a1" test.txt
a1
a10
```
`string $` and `^ string *`
```
[root@vm ~]# grep "10*$" test.txt
a1
a10
```
`string1 \| string2`
```
[root@vm ~]# grep "b\|a5" test.txt
a5
```
## sed
> A Unix utility that parses and transforms text, using a simple, compact programming language. 
### How to work in sed
![](https://github.com/oxolll/Linux/blob/Linux%E7%B3%BB%E7%B5%B1%E8%87%AA%E5%8B%95%E5%8C%96%E9%81%8B%E7%B6%AD/awk%2C%20grep%2C%20sed/sed%E9%81%8B%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9C%96.png)
### Format
`sed 's/regexp/replacement/g' inputFileName > outputFileName`
-----------------------------
#### Common Options
`-n` using silent mode, meaning no data will be output except which has dealt with by special process data\
`-e` using edit mode, the data will be procesed by command\
`-f` ?\
`-r∶sed` ?\
`-i` write to the target file
#### Common Command
`a` add new line after target line\
`c` replace your target by new value\
`d` delete your target \
`i` insert new line before your target\
`p` print target line, usually use `-n` together\
`s` format is `s/yourtarget/yourgoal/g`, replace yourtarget with yourgoal
example1:\
raw data:
```
[root@vm ~]# cat test.txt
a1
a2
a3
a4
a5
a6
a7
a8
a9
a10

```
================ splitor ================================================\
output data:
```
[root@vm ~]# sed '1a a-add line!' test.txt |sed '4c c-line'|sed '5i i-insert line!'|sed -n '1,$p'|sed '11d'|awk '{print NR". "$0}'
1. a1
2. a-add line!      --> sed '1a a-add line!'
3. a2 
4. c-line           --> sed '4c c-line'
5. i-insert line!   --> sed '5i i-insert line!'
6. a4
7. a5
8. a6
9. a7
10. a8
11. a10
                    --> sed -n '1,$p'
                    --> sed '11d'
```
> using the following commands to deal with the data

`sed '1a a-add line!'` add new line after raw 1 \
`sed '4c c-line'` change raw 4 to c-line (replace)\
`sed '5i i-insert line!'` insert new line before raw 5\
`sed -n '1,$p'` print data raw 1 to end but no repeat the data two times (using -n)\
`sed '11d'` delete the raw 11 (output data lost a9)

===========================================================================\
example2:\
raw data:
```
[root@vm ~]# cat test.txt
a1
a2
a3
a4
a5
a6
a7
a8
a9
a10
```
================ splitor ================================================\
output data:
```
[root@vm ~]# sed 's/a5/new!/g' test.txt > new.txt
[root@vm ~]# cat new.txt
a1
a2
a3
a4
new!    -> replace a5 with new!
a6
a7
a8
a9
a10

```
> using the following commands to deal with the data

`sed 's/a5/new!/g' test.txt` replace contain string 'a5' lines with 'new!'\
`test.txt > new.txt` write to new.txt
## Reference
[鳥哥的 Linux 私房菜 第十一章、正規表示法與文件格式化處理](http://linux.vbird.org/linux_basic/0330regularex.php)\
[Regular expression From Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Regular_expression)\
[Linux中 sed 和 awk的用法詳解](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/392291/)\
[AWK From Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/AWK)\
[Awk教學](http://tw.gitbook.net/awk/index.html)\
[sed From Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Sed)\
[三剑客之Sed关于 p、a、d、w、i 、c 模式的干货](https://blog.csdn.net/Sunny_Future/article/details/80174530)\
[[Linux] 檔案文件字串處理-sed 的用法](https://charleslin74.pixnet.net/blog/post/419884144)\
[sed](https://zh.wikipedia.org/wiki/Sed)\
[sed簡介](https://www.itread01.com/p/154537.html)