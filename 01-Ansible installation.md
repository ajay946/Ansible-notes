# Ansible installation
>Here we will be using two machine, one client and one server

**Installing ansible on server**
- sudo su -
- sudo add-apt-repository ppa:ansible/ansible-2.8
- sudo apt-get update
- sudo apt-get install ansible

**Create user in both client and server**
- useradd -m ansible

**Add client IP address to the server(default inventory file)**
- vi /etc/ansible/hosts
>add the client ip address at the end of the file

```
[devops]
13.233.237.128
```

**Give sudo privilages to both client and server**
- visudo
>under memeber of admin group add the following code
```
ansible ALL=(ALL) NOPASSWD: ALL
```

**Create ssh key in server and share the public key with the client**
- ssh-keygen
>copy the key from path provided(id_rsa.pub)
>paste the key in /.ssh/authorized_keys under client

- mkdir .ssh
- cd .ssh
- vi authorized_keys
>paste the key here


**Ping ansible client from ansible server**
- ssh ansible@13.233.237.128


**To check if client is added to the list**
- ansible -m ping all
