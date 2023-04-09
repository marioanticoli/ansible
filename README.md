## Inventory 

inventory.ini 

```
[vpn:vars]
ansible_become_pass='{{ password }}'

[vpn]
myname ansible_host=xxx.xxx.xxx.xxx

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

## Commands

Show inventory

```
ansible-inventory --list -y -i inventory.ini
```

Execute command on group of servers

```
ansible vpn -a "uptime" -i inventory.ini 
```

Execute user playbook

```
ansible-playbook --ask-vault-password --extra-vars '@library/vault.yaml' --ask-pass library/user.yaml
```

Execute ufw playbook

```
ansible-playbook --ask-vault-password --extra-vars '@library/vault.yaml' library/ufw.yaml
```

Execute wireguard playbook

```
ansible-playbook --ask-vault-password --ask-become-pass --extra-vars '@library/vault.yaml' library/wireguard.yaml
```

Execute ssh playbook

```
ansible-playbook --ask-vault-password --extra-vars '@library/vault.yaml' library/ssh.yaml
```
