## Compliance as Code

Compliance as code as the name implies we are writing set of compliance-controls as the code To achieve compliance as code I have used `Inspec` tool Instead of writing the controls on my own I have used premade compliance check written by the community. I have used  `devsec linux profile` to check my Infrastructure against the CIS compliance


## Github Actions

```
name: Compliance as code 

on:
  push:

jobs:
  checkout-repo:
    runs-on: ubuntu-latest
    steps:
    - name : Installing Inspec  
      run : |
        curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P inspec
        inspec version 
    - name: Setting up chef 
      run : |
           echo "$SSH_KEY" >  pentest_key
           chmod 600 pentest_key
           inspec exec https://github.com/dev-sec/linux-baseline --key-files <key-location> --target ssh://root@$IP --chef-license accept
           
           
           
      env:
        SSH_KEY: ${{secrets.KEY}}
        IP: ${{secrets.IP}}

```

## Reference 

1. https://github.com/dev-sec/linux-baseline
2. https://docs.chef.io/inspec/install/