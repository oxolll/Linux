# rsync(reomte synchronize) & Inotify

# rsync
## Introduction
Synchronizes files and folders from one location to another.

Rsync is implemented to update a production host from a development machine.
Using a cron job to call rsync can regularly back up data to a storage location.

[Introduction to rsync | Linode](https://www.linode.com/docs/tools-reference/tools/introduction-to-rsync/)

### Incremental Backup
* Rsync is an incremental tool.
Once the initial operation has completed, the successive backup operations will complete very quickly.

* Only the differences between the source and the destination files are copied.

## Pre work
* check openssh-server on
* stop firewall-server 
* check Selinux (getenforce) off

## Command

### Install
* install rsync : `yum install -y rsync`

### Setting
* Server\
setup the document : `vi /etc/rsyncd.conf`\
![](https://github.com/oxolll/Linux/blob/Linux%E7%B3%BB%E7%B5%B1%E8%87%AA%E5%8B%95%E5%8C%96%E9%81%8B%E7%B6%AD/rsync/setting%20of%20rsyncd.conf.png)\
add user : `useradd -s /sbin/nologin -M rsync`\
make a folder : `mkdir rsync_test`\
change owner and group : `chown rsync.rsync rsync_test`\
make password documet : `touch /etc/rsync.passwd`\
input a set of account and password : `echo "rsync_backup:test" > /etc/rsync.passwd`\
change permission : `chmod 600 /etc/rsync.passwd`\
start rsync : `rsync --daemon`

* Client\
make password documet : `touch /etc/rsync.passwd`\
input a set of account and password : `echo "rsync_backup:test" > /etc/rsync.passwd`\
change permission : `chmod 600 /etc/rsync.passwd`

### Argument
using `-a` to recursively backup under the folder's files and diractors \
using `-v` to get details \
using `-h` to get legible form of numbers

using `--bwlimit=100K` to limit bandwidth\
using `-e 'ssh -p 12345'` to change default port:22 to 12345\
using `--progress` to display remaining time, transmiting progress and speed\
using `--delete` to delete the files which are not in the resources' folders in remote

using `--exclude '*.txt'` to exclude files that have `'.txt'`\
using `--include '*.c'` to include files that have `'.c'`

The command will include the files that have `'.c'` , including subdirectories exclude other\
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
[Linux 使用 rsync 遠端檔案同步與備份工具教學與範例](https://blog.gtwang.org/linux/rsync-local-remote-file-synchronization-commands/)\
[关于 rsync 中: 和 :: 及 rysnc 和 ssh 认证协议的区别](https://cloud.tencent.com/developer/article/1043373)\
[Rsync daemon服務器端安裝配置步驟](http://www.trfoor.com/2020/02/27/rsync-daemon%E6%9C%8D%E5%8B%99%E5%99%A8%E7%AB%AF%E5%AE%89%E8%A3%9D%E9%85%8D%E7%BD%AE%E6%AD%A5%E9%A9%9F/)

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
install inotify(two ways)
* using yum to download :  `yum install -y inotify-tools` 
* using tar to install : 
 1. download the source files -> `wget http://jensd.be/download/inotify-tools-3.14.tar.gz`
 2. using tar to install -> `tar -zxf inotify-tools-3.13.tar.gz `
 3. enter the folder -> `cd inotify-tools-3.14`
 4. setting configure -> `./configure`
 5. `make`
 6. install -> `make install`

The command `inotify -mrq /root/rsync_test --timefmt "%d-%m-%y %H:%M" -format "%T %w%f 事件訊息: -e" -e [open/create/delete/move/attrib/access/modify/close]`
> important argument

using `-m` to keep listening for events forever\
using `-d` to run in the background\
using `-r` to watch directories recursively\
using `-q` to print less (only print events)\
using `-timefmt` to set timeout format
> %[mdyHM] argument
1. m is month
2. d is day
3. y is year
4. H is hour
5. M is minute

using `-format` to set standard output
> %[wfeT] argument
1. w : display filename or directory
2. f : display message 
3. e : event
4. T : display timefmt

using `-e` to listen for specific event(s)
> if omitted, all events are listened for.
> Events
 1. attrib : files or directory attributes changed 
 2. access : files or directory contents were read
 3. create : create within watched directory
 4. delete : delete within watched directory
 5. move : move to or feom watched directory
 6. modify : contents were written
 7. open : files or directory opened
 8. close : files or directory closed

--- 

## rsync + inotify

write a script(/test.sh)
``` 
#!/bin/bash
Path=/root/rsync_data
backup_Server=192.168.154.128

/usr/bin/inotifywait -mrq --format '%w%f' -e create,close_write,delete $Path  | while read line  
do
    if [ -f $line ];then
        rsync -az $line --delete rsync_backup@$backup_Server::backup --password-file=/etc/rsync.passwd
    else
        cd $Path &&\
        rsync -az ./ --delete rsync_backup@$backup_Server::backup --password-file=/etc/rsync.passwd
    fi

done
``` 
change permission : `chmod +x /test.sh`\
run the script in client : `sh /test.sh`\
enter the directory : `cd rsync_data`\
make new file(in client) : `touch {1..6}.txt`\
![](https://github.com/oxolll/Linux/blob/Linux%E7%B3%BB%E7%B5%B1%E8%87%AA%E5%8B%95%E5%8C%96%E9%81%8B%E7%B6%AD/rsync/rsync%20%2B%20inotify.png)\
vm(192.168.154.128) -> Server
vm1(192.168.154.129) -> Client
> vm : /rsync_test -> vm1 : /rsync_data

## References
[inotify - Wikipedia](https://en.wikipedia.org/wiki/Inotify)\
[Use inotify-tools on CentOS 7 or RHEL 7 to watch files and directories for events](http://jensd.be/248/linux/use-inotify-tools-on-centos-7-or-rhel-7-to-watch-files-and-directories-for-events)\
[Linux运维：rsync+inotify实时同步](https://segmentfault.com/a/1190000018096553)
