# Steps to install kong gateway using Ansible role

### step 1:- create a new directory for kong gatewat in work directory 
```
mkdir /home/user/kong_gateway
cd /home/user/kong_gateway
```

### step 2:- inside kong_gateway create following given directory structure 
```
kong_gateway/
|-- roles/
|   `-- kong/
|       |-- tasks/
|       |   |-- main.yml
|       |-- templates/
|       |   `-- kong.service.j2
|       `-- meta/
|           `-- main.yml
`-- playbook.yml

```
### step 3:- Write below given content in roles/kong/tasks/main.yml
```
---
- name: Install required dependencies
  apt:
    name: "{{ item }}"
    state: present
  with_items:
    - unzip
    - libssl-dev
    - libexpat1-dev
    - libyaml-dev
    - liblua5.1-dev
    - lua-socket
    - lua-sec
    - lua-zlib
    - lua-json
    - lua-cjson
    - build-essential

- name: Download and extract Kong source
  become: yes
  get_url:
    url: https://github.com/Kong/kong/archive/2.8.0.tar.gz
    dest: /tmp/kong.tar.gz
    validate_certs: no

- name: Extract Kong source
  become: yes
  unarchive:
    src: /tmp/kong.tar.gz
    dest: /opt
    remote_src: yes
  notify: Restart Kong Service

- name: Set up Kong auto-start script
  template:
    src: kong.service.j2
    dest: /etc/systemd/system/kong.service
      # notify: Restart Kong Service

- name: Ensure Kong is running
  systemd:
    name: kong
    state: started
    enabled: yes

- name: Restart Kong Service
  systemd:
    name: kong
    state: restarted
    enabled: yes
```

### step 4:- write below given content in roles/kong/templates/kong.service.j2
```
[Unit]
Description=Kong API Gateway
After=network.target
After=postgresql.service

[Service]
Type=simple
User=kong
ExecStart=/opt/kong-2.8.0/bin/kong start
ExecReload=/opt/kong-2.8.0/bin/kong reload
ExecStop=/opt/kong-2.8.0/bin/kong stop
Restart=always

[Install]
WantedBy=default.target

```

### step 5:- Now in last insert following code in playbook.yml to call kong role 
```
---
- name: Install Kong Gateway
  hosts: localhost
  connection: local
  become: yes
  roles:
    - kong
```
### step 6:- Finally run playbook on target host 
```
ansible-playbook playbook.yml
```
