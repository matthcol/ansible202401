# Ansible

## Infra

### Build and start hosts (docker)
```
docker compose up -d

docker compose build host4
docker compose up host4 -d
```


### Bash on pilot host (host1)
docker compose exec -it host1 bash

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
