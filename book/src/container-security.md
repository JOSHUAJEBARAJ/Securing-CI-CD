# Container Security

Now days most applications are deployed in a containerized manner We have to make sure the container that used for deploying the application is also secure

To Secure the Docker container I am going to use the below two tools


| Tools       | Uses                                                 |
|-------------|------------------------------------------------------|
| hadolint    | Scans the Dockerfile and suggest the best practices for building the Docker container from the Dockerfile securely|
| docker scan | Scan for security flaws in the Docker Image  that created from the Dockerfile        |


## Github Actions

```
name: Container Scan 

on:
  push:

jobs:
  checkout-repo:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout 🛎️
      uses: actions/checkout@v2
    - name : Scanning for docker image 
      run : |
        docker build -t test .
        docker scan test
    - name : Scanning for Dockerfile 
      if: ${{ always() }}
      run : |
        docker run --rm -i hadolint/hadolint < Dockerfile
```

## References 

1. https://github.com/hadolint/hadolint
2. https://docs.docker.com/engine/scan/
   