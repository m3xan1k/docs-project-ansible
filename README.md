**SETUP SSH**

Can look like this


1. Generate key for ansible

```
ssh-keygen -t rsa -f ~/.ssh/ansible
```


2. Create new user on each server

```
for server in xxx.xxx.xxx.xxx yyy.yyy.yyy.yyy ййй.ййй.ййй.ййй 
do
    ssh "osboxes@$server" "sudo useradd -d /home/ansible -m -s /bin/bash -G sudo ansible"
done
```


3. Setup ansible user password on each remote server

```
ssh osboxes@$server
sudo passwd ansible
```


4. Add identity for each server

```
for server in 192.168.1.105 192.168.1.207 192.168.1.236
do
    ssh-copy-id -i ~/.ssh/ansible.pub "ansible@$server"
done
```


**SETUP ENV**

Can be like this

```
export ANSIBLE_SUDO_PASS=$PASSWORD_FOR_ANSIBLE_USER
```

or with `.env` file

```
export $(cat .env | xargs)
```


**SETUP INVENTORY FILE**

Fill `inventory/hosts` file


**USE PLAYBOOKS**

```
ansible-playbook -i inventory/hosts <filename>.yml
```