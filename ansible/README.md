# ansible

## Introduction
> What is ansible? \
Ansible is an open-source software provisioning, configuration management, and application-deployment tool enabling infrastructure as code.
Control machine
## Inventory
- Like a list of managed node, contain domainname, ipaddr, port, etc.. \
- default path is `/etc/ansible/hosts` \
- you can also edit the setting in `/etc/ansible/ansible.conf`
```
[defaults]

# some basic default values...

#inventory      = /etc/ansible/hosts           --> set inventory
#library        = /usr/share/my_modules/
#module_utils   = /usr/share/my_module_utils/
#remote_tmp     = ~/.ansible/tmp
#local_tmp      = ~/.ansible/tmp
#plugin_filters_cfg = /etc/ansible/plugin_filters.yml
#forks          = 5
#poll_interval  = 15
#sudo_user      = root
#ask_sudo_pass = True

```
look above example of setting of nodes
```
[app1]
192.168.154.129
[app2]
192.168.154.130
[app]
192.168.154.129
192.168.154.130
[local]
localhost ansible_connection=local

```
[app] means a group name app, has two nodes(154.129, 154.130)
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

## Playbook (ansible's script)
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

example :
```
[root@vm ~]# cat test.yml
---

- name: say 'test'
  hosts: app1
  tasks:

    - name: echo 'test'
      command: echo 'it is a test'
      register: result

    - name: print stdout
      debug:
        msg: "{{ result.stdout }}"

```
============================= splitor ================================\
execute...
```
[root@vm ~]# ansible-playbook test.yml

PLAY [say 'test'] **************************************************************

TASK [Gathering Facts] *********************************************************
ok: [192.168.154.129]

TASK [echo 'test'] *************************************************************
changed: [192.168.154.129]

TASK [print stdout] ************************************************************
ok: [192.168.154.129] => {
    "msg": "it is a test"
}

PLAY RECAP *********************************************************************
192.168.154.129            : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0


```
## preset
vi /etc/hosts
ssh-keygen
ssh-copy-id root@192.168.x.x
yum install -y ansible

## command 
ansible app1 -m command "ls /root/"

### Reference
[現代 IT 人一定要知道的 Ansible 自動化組態技巧 06. 怎麼操作 Ansible？](https://chusiang.gitbooks.io/automate-with-ansible/content/06.how-to-use-the-ansible.html)\
