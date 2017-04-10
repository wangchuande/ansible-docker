Docker for Ansible
==================

A project for deploying and configuring [Docker](https://www.docker.com/) on unix hosts using [Ansible](https://github.com/ansible/ansible).

It can additionally be used as a playbook for quickly provisioning hosts.

Supports
--------
Supported Docker versions:

- Docker 17.03.1

Supported targets:

- Ubuntu 16.04 "xenial"
- Ubuntu 16.10 "yakkety"


Usage
-----
Clone this repo:

    $ git clone https://github.com/wangchuande/ansible-docker.git
    
Change `group_vars/docker/vars` user to your server user: 

```
---
remote_user: your_user
ansible_user: your_user
ansible_ssh_pass: "{{ vault_ansible_ssh_pass }}"
ansible_become: true
ansible_become_pass: "{{ vault_ansible_become_pass }}"
```

Delete `group_vars/docker/vault`, and recreate, add your ssh and sudo password:

```
---
vault_ansible_ssh_pass: your_ssh_password
vault_ansible_become_pass: your_sudo_password
```
Encrypt your file:

```
ansible-vault encrypt  inventories/develop/group_vars/docker/vault
```


Add hosts to `inventories/develop/hosts` docker group

    [docker]
    192.168.200.91
    
export your vault file password:
`export VAULT_PASSWORD=your_vault_password`

Run the command:

    ansible-playbook deploy-docker.yml -i inventories/develop

or just run the script:

    ./deploy-docker.sh
