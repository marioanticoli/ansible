## Inventory 

inventory.ini 

```
[vpn:vars]
ansible_become_pass='{{ password }}'

[vpn]
myname ansible_host=xxx.xxx.xxx.xxx ansible_ssh_pass={{ root_pass }}

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

## Vault
`library/vault.yaml` should set the following variables:

- username
- password
- salt
- public_key
- wg_server_privkey
- wg_server_pubkey
- root_pass

## Commands

Edit vault 

```
ansible-vault edit vault.yaml
```

Show inventory

```
ansible-inventory --list -y -i inventory.ini
```

Execute command on group of servers

```
ansible vpn -a "uptime" --extra-vars '@library/vault.yaml' --ask-vault-password -i inventory.ini
```

Execute user playbook

```
ansible-playbook --ask-vault-password --extra-vars '@library/vault.yaml' library/user.yaml
```

Execute ufw playbook

```
ansible-playbook --ask-vault-password --extra-vars '@library/vault.yaml' library/ufw.yaml
```

Execute ssh playbook

```
ansible-playbook --ask-vault-password --extra-vars '@library/vault.yaml' library/ssh.yaml
```

Execute wireguard playbook

```
ansible-playbook --ask-vault-password --ask-become-pass --extra-vars '@library/vault.yaml' library/wireguard.yaml
```

# TODO

Refactor into roles
