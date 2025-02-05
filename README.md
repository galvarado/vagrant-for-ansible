# Vagrant for ansible

 A vagrant environment for running an Ubuntu 22.04 ready to test ansible commands/playbooks.
 
Since Vagrant provides easy to configure, reproducible, and portable work environments, this setup helps you create ansible playbooks in a safe environment using vagrant emulating real environments.

It is ready to run ansible just by starting the environment, the repository contains a preconfigured ```inventory``` ready to work with the target host. We use an Ubuntu 22.04 instance and the default ```vagrant``` user to log in.

## How to use

### Prerequisites


- Install [Vagrant](https://www.vagrantup.com/docs/installation) and [Virtualbox](https://www.vagrantup.com/docs/providers/virtualbox).
- Have an ssh key located at: ```~/.ssh/id_rsa.pub```

### Spin up the environment

Start vagrant target host:

```
$ vagrant up
```
### Start writting ansible

Run ansible:

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

You will find a collection of playbooks in their directory ready to use them. The playbook target is defined as a variable. To match the current Vagrant host you need pass the target as follows:

```
ansible-playbook -i inventory  playbooks/addcronjob.yaml --extra-vars "target=myhosts" 
```

Output:

```
PLAY [myhosts] ******************************************************************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************************************************************
ok: [192.168.56.10]

TASK [cron] *********************************************************************************************************************************************************************************************************
ok: [192.168.56.10]

PLAY RECAP **********************************************************************************************************************************************************************************************************
192.168.56.10              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

 More information about targeting hosts and groups: https://docs.ansible.com/ansible/latest/user_guide/intro_patterns.html


#### Debug

You can ssh into the vm with:

```
vagrant ssh
```

Or using a default ssh client:

```
ssh vagrant@192.168.56.10
```

### Ansible provisioner

To run ansible adhoc commands the best option is use the previous approach that simulate a real environment.  But you can also use the [Ansible provisioner](https://www.vagrantup.com/docs/installation) that uses a different approach, it will run on the provisioning phase of vagrant. 