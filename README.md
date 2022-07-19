# Vagrant for ansible

This repository helps to create ansible playbooks in a safe environment using vagrant to create a VM target where you can test ansible playbooks and commands without having important consequences since Vagrant provides easy to configure, reproducible, and portable work environments.


It is ready to run ansible just by starting the environment, there is a preconfigured inventory with the myhosts group where the vagrant VM is located. The default user vagrant is used and an ssh key is copied when you start vagrant, you only need to have a key in .ssh/id_rsa.pub



## How to use


### Prerequisites

Install [Vagrant](https://www.vagrantup.com/docs/installation) and [Virtualbox](https://www.vagrantup.com/docs/providers/virtualbox).

Official documentation: https://www.vagrantup.com/downloads

*To achieve its magic, Vagrant stands on the shoulders of giants. Machines are provisioned on top of VirtualBox, VMware, AWS, or any other provider. 

### Spin up the environment

Start the environment:

```
$ vagrant up
```
### Start writting ansible

run ansible:
```
$ ansible -i inventory -m ping myhosts
```

Output:
```
192.168.56.10 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

You can ssh into the vm with:

```
vagrant ssh
```

Or using a default ssh client:

```
ssh vagrant@192.168.56.10
```
