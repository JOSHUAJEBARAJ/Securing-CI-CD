# SAST SCAN

In this SAST scan we are going to scan through the application source code for security flaws

Since the application is based on **Python** I am going to use the tool called [bandit](https://pypi.org/project/bandit/)

## Github actions

```
name: sast 

on:
  push:

jobs:
  checkout-repo:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout 🛎️
      uses: actions/checkout@v2
    - name : Installing the bandit tool
      run : |
        pip install bandit
        bandit -r app 
```


## References

1. https://pypi.org/project/bandit/