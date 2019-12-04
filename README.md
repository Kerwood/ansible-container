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

### Ansible Playbook
Same principle with the `ansible-playbook` command. Just remove the `--entrypoint=ansible` paramenter.
```
docker run --rm -it \
    -v ~/.ssh/id_rsa:/root/.ssh/id_rsa \
    -v $(pwd):/ansible/playbooks \
    ansible playbook.yml --inventory=hosts.ini
```  

### Create alias
Here's two examples on alias, that mounts your SSH key inside the container to use for your servers.  
With these you can use the ansible container as normal commands. The container becomes transparent.
```
alias ansible='docker run --rm -it -v $(pwd):/ansible/playbooks -v ~/.ssh:/root/.ssh --entrypoint=ansible ansible'
alias ansible-playbook='docker run --rm -it -v $(pwd):/ansible/playbooks -v ~/.ssh:/root/.ssh  ansible'
```

Example:
```
ansible all -m ping --inventory-file=hosts
```