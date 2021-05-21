# Secret-Scanning

Developers often tends to embed the sensitive information like apikeys,passwords  and push it to the code-base When the attacker able to get access to the sensitive information they can use these credentials and abuse the application 

To prevent the secret pushed into the code base we are going to use the tool called [truffleHog](https://github.com/trufflesecurity/truffleHog) which scans the repository for sensitive information like passwords,API keys

> Note The above technique I am using is only to able to scan for the secrets in the source-control after it is pushed  Ideally you should have precommit hooks inorder to prevent the code being commit  

TruffleHog is the python based tool used to scan the repositories the sensitive information

## Github Action

```
name: secret-scanning

on:
  push:

jobs:
  checkout-repo:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout 🛎️
      uses: actions/checkout@v2
    - name : Installing secret-scanning tool
      run : |
        pip3 install truffleHog
        truffleHog --regex --entropy=False .
```
## References

1. https://github.com/trufflesecurity/truffleHog