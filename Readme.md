# Ansible

## Infra

### Build and start hosts
docker compose up -d

### Bash on pilot host (host1)
docker compose exec -it host1 bash

## Install Ansible
apt install ansible sshpass

## Ansible CLI
### Help
`ansible --help`

### Module ping
(no password, need ssh key)
`ansible -i hosts -m ping all`

```
ansible -i hosts -k -m ping all
ansible -i hosts -u srvadmin -k -m ping all
ansible -i hosts -u srvadmin -k -m ping servers12
ansible -i hosts -u srvadmin -k -m ping "*12"
ansible -i hosts -u srvadmin -k -m ping '!servers11'
```

### Module user
```
ansible -i hosts -u srvadmin -k -b -K -m user -a "name=ender" all
ansible -i hosts -u srvadmin -k -b -K -m user -a "name=ender state=absent remove=true" all
```