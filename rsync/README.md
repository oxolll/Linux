# rsync(reomte synchronize)

## Introduction

Synchronizes files and folders from one location to another\

Be implemented using rsync are updating a production host from a development machine, or using a cron job to call rsync to regularly back up data to a storage location.\

### Incremental Backup
*Rsync is incremental, so once the initial operation has completed, successive backup operations complete very quickly\

*Only the differences between the source and the destination files are copied\

## Pre work
* check openssh-server on
* stop firewall-server 
* check Selinux (getenforce) off

## Command

* install rsync : `yum install -y rsync`

### Copy like command "cp -r"
* copy file from /tmp/test.txt to /tmp2 : `rsync -avh /tmp/test.txt /tmp2`\
using `-a` recursively backup under the folder's files and diractors \
using `-v` get details \
using `-h` get good-reading form of numbers

### Remote backup like command "scp -r"
Default setting ssh to login remote machine\
* backup file from /tmp/test.txt to [hostname]@[ip address]/tmp2/backup/ : `rsync -avh /tmp/test.txt root@192.168.154.129:/tmp2`\

* backup file from [hostname]@[ip address]/tmp2/backup/ to /tmp/ : `rsync -avh  root@192.168.154.129:/tmp2 /tmp2`


## Reference
[Introduction to rsync | Linode](https://www.linode.com/docs/tools-reference/tools/introduction-to-rsync/)\
[Linux 使用 rsync 遠端檔案同步與備份工具教學與範例](https://blog.gtwang.org/linux/rsync-local-remote-file-synchronization-commands/)\
[关于 rsync 中: 和 :: 及 rysnc 和 ssh 认证协议的区别](https://cloud.tencent.com/developer/article/1043373)\
[Linux运维：rsync+inotify实时同步](https://segmentfault.com/a/1190000018096553)