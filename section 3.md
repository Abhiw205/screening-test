# Steps to install kong gateway using Ansible role

### steps 1:- create a new directory for kong gatewat in work directory 
```
mkdir /home/user/kong_gateway
cd /home/user/kong_gateway
```

## steps 2:- inside kong_gateway create following given directory structure 
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
