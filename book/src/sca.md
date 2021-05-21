# SCA

SCA stands for the Source Composition Analysis here we are scanning the dependency (eg library) used in the application for security vulnerabilities

Since the application is based on the python I am going to use [Pyraider](https://pypi.org/project/pyraider/) tool which helps  

## Github actions 
Below is the Github action for performing the SCA

```
name: sca

on:
  push:

jobs:
  checkout-repo:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout 🛎️
      uses: actions/checkout@v2
    - name : Installing the sca
      run : |
        pip install pyraider
        cd app
        pyraider check -f requirements.txt
```

## References

1. https://pypi.org/project/pyraider/