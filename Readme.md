# Ansible

## Infra

### Build and start hosts (docker)
```
# build and start all
docker compose up -d

# rebuild host 5
docker compose build host5

# (re)create host5
docker compose up host5 -d
```


### Bash on pilot host (host1)
docker compose exec -it host1 bash

### Ssh commands
```
ssh host2
ssh srvadmin@host2
ssh -i ~/.ssh/id_rsa_ender ender@host2

ssh-keygen

# start ssh agent
ssh-agent
# copy-paste output ssh-agent

# unlock identity
ssh-add  ~/.ssh/id_rsa_ender

# list identities
ssh-add -L 

# remove all identities
ssh-add -D

```

## Install Ansible
apt install ansible sshpass

## Ansible CLI
### Help
`ansible --help`

### Module ping
(no password, need ssh key)

```
ansible -i hosts -m ping all
```

(with password for user SSH)
```
ansible -i hosts -k -m ping all
ansible -i hosts -u srvadmin -k -m ping all
ansible -i hosts -u srvadmin -k -m ping servers12
ansible -i hosts -u srvadmin -k -m ping "*12"
ansible -i hosts -u srvadmin -k -m ping '!servers11'
```

### Module user
(need to become root in target hosts, method=sudo with password)
```
ansible -i hosts -u srvadmin -k -b -K -m user -a "name=ender" all
ansible -i hosts -u srvadmin -k -b -K -m user -a "name=ender state=absent remove=true" all
```

## First Playbook
(with current user=srvadmin, become root with sudo is set in the playbook, still need SSH password and sudo password )
```
 ansible-playbook -i hosts -k -K create_user_playbook.yml
 ```

(with user SSH ender and SSH key unlocked)
```
 ansible-playbook -i hosts -u ender playbook.yml

 # debug
 ansible-playbook -i hosts -u ender -v playbook.yml
 ansible-playbook -i hosts -u ender -vv playbook.yml
 ansible-playbook -i hosts -u ender -vvv playbook.yml
 ```

 ## Playbook with roles
 ### Create role(s) tree
 ```
ansible-galaxy init roles/common
ansible-galaxy init roles/app
ansible-galaxy init roles/db
 ```

 ## Links
 ### Playbook syntax
 - https://docs.ansible.com/ansible/latest/playbook_guide/playbooks.html
 ### Builtin Modules
 - https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html
 ### Community Collections
 - https://docs.ansible.com/ansible/latest/collections/community/postgresql/index.html

 ## Ansible Configuration

 Create empty config file (as root)

 ```
 ansible-config init --disabled > /etc/ansible/ansible.cfg

# content:
[defaults]
allow_world_readable_tmpfiles=yes
interpreter_python=/usr/bin/python3

 ```

NB: links
- https://docs.ansible.com/ansible/latest/installation_guide/intro_configuration.html
- https://docs.ansible.com/ansible/latest/reference_appendices/interpreter_discovery.html

