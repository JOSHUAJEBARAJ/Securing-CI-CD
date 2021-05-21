# Container Security

Now days all application are deployed in the containerized manner We have to make sure the container is also very secure

To secure  the Container I am going to use the two tools


| Tools       | Uses                                                 |
|-------------|------------------------------------------------------|
| hadolint    | Scans the Docker file and suggest the best practices |
| docker scan | Scan for security flaws in the docker Image          |


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
   