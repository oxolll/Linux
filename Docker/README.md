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
<<<<<<< HEAD
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
### [chroot](https://windsock.io/a-basic-container/)
=======
1. UTS namespace(Unix Time-sharing):
2. IPC namespace(Inter-Process Communication):
3. PID namespace(Process ID):
4. mount namespace:
5. network namespace:
6. user namespace:
### hroot
>>>>>>> ad98537f452933bcda5d21be7c41dff2f48544de
### Control group

## Install

