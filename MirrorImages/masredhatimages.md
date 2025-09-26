## Mirroring Red Hat Images

```
[ibmmas/cli:15.6.1]mascli$ mas mirror-redhat-images
IBM Maximo Application Suite Air Gap Red Hat Image Mirror (v15.6.1)
Powered by https://github.com/ibm-mas/ansible-devops/


1) Configure Mirror Mode
Working Directory > /mnt/registry
Mirror Mode:
  1. Direct
  2. To filesystem
  3. From filesystem
Select Mirror Mode > 1


2) Configure Images to Mirror

2.1) Select OCP Release
Select the release to mirror content for:
Supported OCP Releases:
  1) 4.18
  2) 4.17
  3) 4.16
  4) 4.15
  5) 4.14

Select OCP Release > 2


3) Configure Target Mirror
Mirror Registry Host > avregistry1.fyre.ibm.com
Mirror Registry Port > 5000
Mirror Registry Prefix >
Mirror Registry Username > *****
Re-use saved registry password? [Y/n] y


4) Configure Red Hat Authentication
Path to your Red Hat pull secret, available from:
  - https://console.redhat.com/openshift/install/pull-secret

Red Hat Pull Secret > /mnt/home/pull-secret.dms

4.1) Red Hat OCP Release
Mirror the Red Hat OCP release to your registry, you must select the mininum and maximum version of the release that you want mirrored.

Images will be mirrored to:
  - avregistry1.fyre.ibm.com:5000/openshift/release
  - avregistry1.fyre.ibm.com:5000/openshift/release-images

An ImageDigestMirrorSet must be configured in the cluster to make use of the mirrored release (see mas configure-airgap)

Mirror Red Hat OCP release [y/N] y
Minimum Version (x.y.z) > 4.17.39
Maximum Version (x.y.z) > 4.17.39

4.2) Red Hat OCP Operator Catalogs
Mirror selected content from the Red Hat OCP operator catalogs to your registry, only the following content will be included from each catalog:

Certified Operators:
 - crunchy-postgres-operator (v5)
 - gpu-operator-certified (v23.3)
 - kubeturbo-certified (stable)

Community Operators:
 - grafana-operator (v4)
 - opentelemetry-operator (alpha)
 - strimzi-kafka-operator (stable)

Red Hat Operators:
 - amq-streams (stable)
 - openshift-pipelines-operator-rh (latest)
 - nfd (stable)
 - aws-efs-csi-driver-operator (stable)
 - local-storage-operator (stable)
 - odf-operator (stable-4.17)

An ImageDigestMirrorSet must be configured in the cluster to make use of the mirrored release (see mas configure-airgap)

Mirror selected content from Red Hat OCP operator catalogs [y/N] y


5) Review Settings

    Configuration
    Mirror Mode ........................... direct
    Working Directory ..................... /mnt/registry
    Authentication ........................ /mnt/home/pull-secret.dms
    Target Registry ....................... avregistry1.fyre.ibm.com:5000

    Red Hat Content
    OpenShift Release ..................... 4.17
    Mirror Release ........................ Yes
    - Minimum Version ..................... 4.17.39
    - Maximum Version ..................... 4.17.39
    Mirror Operator Catalogs .............. Yes

Proceed with these settings [y/N] y


6) Run Mirror Process
Mirroring Red Hat Content ... /mnt/registry/logs/mirror-20250926-120949-redhat.log
....
[SUCCESS] Red Hat Content: /mnt/registry/logs/mirror-20250926-120949-redhat.log
```
