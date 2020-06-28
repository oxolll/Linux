# ansible
Control machine
## Inventory
Like a list of managed node, contain domainname, ipaddr, port, etc.. 
## Ad-Hoc command
- like a simple command
- execute easy task \
example1 : `ping` 
```
[root@vm yum.repos.d]# ansible all -m ping
localhost | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
192.168.154.130 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
192.168.154.129 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}

```
============================= splitor ================================\
example2 : `echo`
```
[root@vm yum.repos.d]# ansible all -m command -a "echo hello world"
localhost | CHANGED | rc=0 >>
hello world
192.168.154.130 | CHANGED | rc=0 >>
hello world
192.168.154.129 | CHANGED | rc=0 >>
hello world
```

## Playbook
- like a shell script
- using YAML format
1. Play
    * Setup a official website with Drupal
    * Restart the API service 
2. Task
    * Install the package
    * Kill the process  
3. Module
    * apt: name=vim state=present (using apt to install vim)
    * command: /sbin/shutdown -r now (using `shutdown -r now` to reboot)


## preset
vi /etc/hosts
ssh-keygen
ssh-copy-id root@192.168.x.x
yum install -y ansible

## command 
ansible app1 -m command "ls /root/"