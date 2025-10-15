Installation:

Error

![pipelineerror](./pipelineerror.png)

this is desite the mas-ibm-catalog idms has an entry for quay.io/ibmmas:

```
    - mirrorSourcePolicy: NeverContactSource
      mirrors:
        - 'avregistry1.fyre.ibm.com:5000/ibmmas'
      source: quay.io/ibmmas
```