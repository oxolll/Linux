# Regular Expression
> Three text processing utilities — awk, grep, sed

## Introduction
-Regular Expression is a sequence of characters that define a search pattern.
-Usually such patterns are used by string searching algorithms for "find" or "find and replace" operations on strings, or for input validation.

## awk
> A tool divide one pattern to more fields each time.
### Format
`awk 'condition1{action 1} condiction2{action2} ...' filename`  
There is a data => value1 value2 value3 value4
if i want to get the second value, i can use `| awk '{print $2}'`\
$0 =>  value1 value2 value3 value4\
$1 => value1\
$4 => value4\
variable	   meaning
    NF	  represent the numbers of the patterns' fields
    NR	  represent the number of which row be delt with now by awk
    FS	  spilt parameter, default value is " "
[AWK From Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/AWK)
## grep

## sed

## Reference
[鳥哥的 Linux 私房菜 第十一章、正規表示法與文件格式化處理](http://linux.vbird.org/linux_basic/0330regularex.php)\
[Regular expression From Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Regular_expression)\