# kojitechs-ansible-fundamental
kojitechs-ansible-fundamental

## Create user using Ad-hoc
```
ansible ubuntu -m user -a "name=ansible create_home=yes" -u ubuntu -b -k -K
```
## Need to set up password for the user
```
ansible ubuntu -m shell -a "echo 'ansible:password' | chpasswd" -u ubuntu -b -k -K
```
## Change user password on linux
```
ansible ubuntu -m shell -a "echo password | password --stdin ansible" -u root -K
```

## check what user was created
```
ansible all -m command -a "id" -u ansible
```