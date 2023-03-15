# Ansible commands
ansible worker -m ping
ansible '*' -m ping
ansible all -m ping -o
ansible controle --list-hosts
/usr/local/bin/ansible all -a 'id' -o 