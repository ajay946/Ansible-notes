# Ansible notes

Execute commands on client from server  

- ansible -m shell -a 'ls' all
>the 'ls' command will be executed on
all clients
simillar way we can execute any command

#### Writing playbook
 >We can refer ansible docs for each module

 we will write a playbook **play.yml** with following modules:
<b>
- update repositories
- install apache2
- copy file from server to client
- Download tomcat
- Unarchive tomcat
- Download Ant_Example
- install unzip
- unzip Ant_Example
</b>

```
-
 hosts: devops
 become: true
 tasks:
   - name: Update repositories cache
     apt:
       update_cache: yes

   - name: install webserver
     apt:
        name: apache2
        state: present
        force_apt_get: yes

   - name: Copy file with owner and permissions
     copy:
        src: /home/ansible/index.html
        dest: /home/ansible
        owner: ansible
        group: ansible
        mode: '0644'

   - name: Download tomcat
     get_url:
       url: https://downloads.apache.org/tomcat/tomcat-7/v7.0.105/bin/apache-tomcat-7.0.105.tar.gz
       dest: /home/ansible
       mode: '0440'

   - name: Unarchive tomcat
     unarchive:
      src: /home/ansible/apache-tomcat-7.0.105.tar.gz
      dest: /home/ansible
      remote_src: yes

   - name: Download ant
     get_url:
       url: http://cdn.dzone.com/static/downloads/vaannila/examples/ant/example/AntExample1.zip
       dest: /home/ansible
       mode: '0440'

   - name: Install the package "unzip"
     apt:
      name: unzip
      state: present
      force_apt_get: yes

   - name: Unarchive antexample
     unarchive:
      src: /home/ansible/AntExample1.zip
      dest: /home/ansible
      remote_src: yes
```

**To run the written yaml playbook script**
- ansible-playbook play.yml
