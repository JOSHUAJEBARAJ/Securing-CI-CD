# SBOM

Software Bill of material is list of components(third party) present in the Code 

To generate the **SBOM** I am going to use [cyclonedx](https://cyclonedx.org/)

I am going to use [CycloneDX Python Module](https://github.com/CycloneDX/cyclonedx-python) to generate the SBOM since the application is based on the python


## Github Action

```
name: sbom 

on:
  push:

jobs:
  checkout-repo:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout 🛎️
      uses: actions/checkout@v2
    - name : Installing the cyclonedx-bom   
      run : |
        pip install cyclonedx-bom  
        cd app
        cyclonedx-py
    - uses: actions/upload-artifact@v1
      with:
        name: report
        path: ${{ github.workspace }}/app/bom.xml
      name: 'Upload Package'
```


## References 

1. https://www.synopsys.com/blogs/software-security/software-bill-of-materials-bom/
2. https://github.com/CycloneDX/cyclonedx-python