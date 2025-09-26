## Mirror images to registry

1. Create the MAS CLI container

```
[root@avregistry1 ~]# podman run -it -v /Images:/mnt/registry -v ~:/mnt/home --name mascli --pull always quay.io/ibmmas/cli
Trying to pull quay.io/ibmmas/cli:latest...
Getting image source signatures
Copying blob 437bcf1d5151 done   |
Copying blob 0df697abec85 done   |
Copying blob 8966e6845693 done   |
Copying blob 1541f2314df8 done   |
Copying blob e94f27ab7a67 done   |
Copying blob 84283e1bfc6f done   |
Copying blob b35615535e7b done   |
Copying config cad2c93436 done   |
Writing manifest to image destination
IBM Maximo Application Suite CLI Container v15.6.1

https://github.com/ibm-mas/ansible-devops
https://github.com/ibm-mas/cli

MAS Management:
  - mas install to install a new MAS instance
  - mas update to apply a new catalog update
  - mas upgrade to upgrade an existing MAS install to a new release
  - mas must-gather to perform must-gather against the target cluster
  - mas uninstall to uninstall a MAS instance
  - mas configtool-oidc to configure OIDC integration
Disconnected Install Support:
  - mas setup-registry to setup a private container registry on an OCP cluster
  - mas teardown-registry to delete a private container registry on an OCP cluster
  - mas mirror-images to mirror container images required by MAS to a private registry
  - mas configure-airgap to configure a cluster to use a private registry as a mirror
OpenShift Cluster Management:
  - mas provision-aws to provision an OCP cluster on AWS
  - mas provision-roks to provision an OCP cluster on IBMCloud Red Hat OpenShift Service (ROKS)
  - mas provision-rosa to provision an OCP cluster on AWS Red Hat OpenShift Service (ROSA)
  - mas provision-fyre to provision an OCP cluster on IBM DevIT Fyre (internal)
AI Service (Standalone) Management:
  - mas aiservice-install to install a new AI Service instance

[ibmmas/cli:15.6.1]mascli$
```

