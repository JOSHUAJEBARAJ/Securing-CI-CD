## Infrastructure security

Even though we tends to use the containers for deployment we have to make sure the underlying Infrastructure is secure .To harden the underlying Infrastructure I am going to use `Ansible-role` which help to harden the underlying Infrastructure

## Github Actions

```

name: Infra-scan 

on:
  push:

jobs:
  checkout-repo:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout 🛎️
      uses: actions/checkout@v2 
    - name : Installing ansible  
      run : |
        sudo apt update
        sudo apt install ansible 
        ansible-galaxy --version
    - name: Setting up the ansible
      run : |
           cd ansible
           echo "$SSH_KEY" >  pentest_key
           chmod 600 pentest_key
           echo "$IP" >> inventory
           ansible-galaxy collection install devsec.hardening
           ansible-playbook playbook.yaml 
           
      env:
        SSH_KEY: ${{secrets.KEY}}
        IP: ${{secrets.IP}}
```


## Reference 

1. https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html

2. https://dev-sec.io/