# rsync(reomte synchronize) & Inotify

# rsync
## Introduction
Synchronizes files and folders from one location to another.

Rsync is implemented to update a production host from a development machine.
Using a cron job to call rsync can regularly back up data to a storage location.

### Incremental Backup
* Rsync is an incremental tool.
Once the initial operation has completed, successive backup operations complete very quickly

* Only the differences between the source and the destination files are copied

## Pre work
* check openssh-server on
* stop firewall-server 
* check Selinux (getenforce) off

## Command

* install rsync : `yum install -y rsync`

### Argument
using `-a` recursively backup under the folder's files and diractors \
using `-v` get details \
using `-h` get good-reading form of numbers

using `--bwlimit=100K` to limit bw\
using `-e 'ssh -p 12345'` to change default port:22 to 12345\
using `--progress` to display commit 進度 speed 剩餘時間\
using `--delete` to delete the files is not in the resources' folder in remote machine

using `--exclude '*.txt'` to exclude the files has `'.txt'`\
using `--include '*.c'` to include the files has `'.c'`

The command will include the files have `'.c'` include in child diractor exclude other\
`rsync -avh --include '*.c' --include '*/' --exclude '*' myfolder/ backup/`\
Notice! `--include` and `--exclude` order can not be chagned\
If you use this command `rsync -avh --exclude '*' --include '*.c' --include '*/'  myfolder/ backup/`,\
you will do nothing !

### Copy like command "cp -r"
* copy file from /tmp/test.txt to /tmp2/ : `rsync -avh /tmp/test.txt /tmp2/`

### Remote backup like command "scp -r"
Default setting ssh to login remote machine
* backup file from /tmp/test.txt to [hostname]@[ip address]/tmp2/backup : `rsync -avh /tmp/test.txt root@192.168.154.129:/tmp2`
* backup file from [hostname]@[ip address]:/tmp2/backup/  to  /tmp/ : `rsync -avh  root@192.168.154.129:/tmp2/backup/ /tmp/`

## References
[Introduction to rsync | Linode](https://www.linode.com/docs/tools-reference/tools/introduction-to-rsync/)\
[Linux 使用 rsync 遠端檔案同步與備份工具教學與範例](https://blog.gtwang.org/linux/rsync-local-remote-file-synchronization-commands/)\
[关于 rsync 中: 和 :: 及 rysnc 和 ssh 认证协议的区别](https://cloud.tencent.com/developer/article/1043373)\
[Linux运维：rsync+inotify实时同步](https://segmentfault.com/a/1190000018096553)

---

# Inotify

## introduction
Extend filesystems to notice changes to the filesystem, and report those changes to applications.

Be used to automatically update directory views, reload configuration files, log changes, backup, synchronize, and upload.

> Limitation
* Does not support recursively watching directories :
A separate inotify watch must be created for every subdirectory.
* Does report some but not all events in `sysfs` and `procfs`.
* Rename events are not handled directly;

## Document
> in the `/proc/sys/fs/inotify/`
- max_user_watches : set the number of files the command `inotifywait` and `inotifywach` can monitor
- max_user_instances : set the number of progress the command `inotifywait` and `inotifywatch` can be used per user
- max_queued_events : 

## Command

* install inotify : `yum install -y inotify-tools` or ``

## References
[inotify - Wikipedia](https://en.wikipedia.org/wiki/Inotify)\