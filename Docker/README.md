# Docker(Containers)

## Introduction

> what is docker(containers)?
- Products of operating system virtualization\
Providing a lightweight virtual environment

- Application containers\
Designed to package and run a single service when you create containers per application

- The isolation guarantees\
Isolate a set of processes and resources such as memory, CPU, disk, etc..

- A layer for the container\
The Layer helps Docker to reduce duplication and increases the re-use

## Three techniques in Docker

### Namespace :
1. [UTS namespace(Unix Time-sharing)](https://windsock.io/uts-namespace/):\
Isolate the hostname and the NIS domain name.
2. [IPC namespace(Inter-Process Communication)](https://windsock.io/ipc-namespace/):\
Isolate System V IPC objects, and POSIX message queues.
3. [PID namespace(Process ID)](https://windsock.io/pid-namespace/):\
Isolates process ID (PID) numbers.
4. [mount namespace](https://windsock.io/mnt-namespace/):\
Isolate a set of mount points for a process or processes 
5. [network namespace](https://windsock.io/net-namespace/):\
Isolate a process in terms of its network stack
6. [user namespace](https://coreos.com/rkt/docs/latest/devel/user-namespaces.html):\
Isolate user policy of its user IDs, group IDs, keys and capabilities
### chroot
[chroot](https://windsock.io/a-basic-container/)
### Control group

## Commands
* download docker : `yum install docker-ce -y` or `curl -sSL https://get.docker.com | sh`\
 using `yum install docker` will download old version of docker
---
* start service : `systemctl start docker`
---
* check version : `docker version`
---
* check docker detail : `docker info`
---
* check docker working : `docker run hello-world`\
 download a test-image and run in a container
---
* 

## Reference
[容器化技術的網路難題，為什麼它是安全的? - 德鴻科技 Grandsys](https://www.grandsys.com.tw/news/rd/901-linux-docker)
[dockerhub](https://hub.docker.com/)
[docker-在-centos7-上安裝-docker並簡單測試應用](https://medium.com/ianyc/docker-%E5%9C%A8-centos7-%E4%B8%8A%E5%AE%89%E8%A3%9D-docker%E4%B8%A6%E7%B0%A1%E5%96%AE%E6%B8%AC%E8%A9%A6%E6%87%89%E7%94%A8-506a6e0767de)
[CentOS 7.5 安裝 Docker 18.06 容器環境](http://www.weithenn.org/2018/08/docker1806-on-centos75.html)
