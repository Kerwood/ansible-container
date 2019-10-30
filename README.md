# ansible-container
Dockerfile for creating an Ansible container
## Build
```
docker build -t ansible .
```

## Run
### Ansible
Run ansible commands like below command, standing in your current playbook directory.
```
docker run --rm -it \
    -v $(pwd):/ansible/playbooks \
    -v ~/.ssh/id_rsa:/root/.ssh/id_rsa \
    --entrypoint=ansible \
    ansible all -m ping --inventory=hosts.ini
```
Or create an alias.
```
alias ansible='docker run --rm -it -v $(pwd):/ansible/playbooks -v ~/.ssh/id_rsa:/root/.ssh/id_rsa --entrypoint=ansible ansible'
```
And run like this.
```
ansible all -m ping --inventory-file=hosts
```

### Ansible Playbook
Same principle with the `ansible-playbook` command. Just remove the `--entrypoint=ansible` paramenter.
```
docker run --rm -it \
    -v ~/.ssh/id_rsa:/root/.ssh/id_rsa \
    -v $(pwd):/ansible/playbooks \
    ansible playbook.yml --inventory=hosts.ini
```  
