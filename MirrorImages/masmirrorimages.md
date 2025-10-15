## Mirror images to registry

1. Create the MAS CLI container, mounting it on `/Images` and where the license file is located (hence there are two mounts)

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

[ibmmas/cli:15.6.1]mascli$ ls /mnt/home
anaconda-ks.cfg  katello-ca-consumer-latest.noarch.rpm	openshift-client-linux-amd64-rhel8.tar.gz  pull-secret.dms  registry_creation.sh
[ibmmas/cli:15.6.1]mascli$ ls /mnt/registry
auth  certs  data  downloads
```
2. Run `mas mirror-images` command

```
[ibmmas/cli:15.6.1]mascli$ mas mirror-images
IBM Maximo Application Suite Air Gap Image Mirror (v15.6.1)
Powered by https://github.com/ibm-mas/ansible-devops/



1) Configure Catalog Version (see https://ibm-mas.github.io/cli/catalogs/ for details on catalogs)
MAS Catalog Version > v9-250902-amd64
MAS Channel > 9.1.x


2) Configure Mirror Mode
Working Directory > /mnt/registry
Mirror Mode:
  1. Direct
  2. To filesystem
  3. From filesystem
Select Mirror Mode > 1


3) Configure Target Mirror
Mirror Registry Host > avregistry1.fyre.ibm.com
Mirror Registry Port > 5000
Mirror Registry Prefix >


4) Configure Authentication
Mirror Registry Username > *****
🔐 Mirror Registry Password >  ********


5) Configure Images to Mirror
Mirror all MAS images (with dependencies) [y/N] n
IBM Maximo Operator Catalog [Y/n] y
IBM Maximo Application Suite - Core [Y/n] y
IBM Maximo Application Suite - Assist [y/N] n
IBM Maximo Application Suite - IoT [y/N] n
IBM Maximo Application Suite - Manage [y/N] y
IBM Maximo Application Suite - Maximo IT (Separately entitled Manage extension) [y/N] n
IBM Maximo Application Suite - Monitor [y/N] n
IBM Maximo Application Suite - Optimizer [y/N] n
IBM Maximo Application Suite - Predict [y/N] n
IBM Maximo Application Suite - Visual Inspection [y/N] n
IBM Maximo Application Suite - Facilities [y/N] n
IBM Foundational Services [Y/n] y
IBM Suite License Service [Y/n]
IBM Truststore Manager [Y/n]
MongoDb Community Edition [Y/n]

MongoDb Community Edition options for mirroring:
  1. Default MongoDb version set by catalog source (recommended)
  2. MongoDb version 4
  3. MongoDb version 5
  4. Mirror all supported MongoDb versions

Select the MongoDb Community Edition mirroring option > 1

IBM Db2 [Y/n] y
IBM Cloud Pak for Data (CP4D) [y/N] n
IBM Watson Studio Local [y/N]
IBM Watson Machine Learning [y/N]
IBM Analytics Engine (Spark) [y/N]
IBM Cognos Analytics [y/N]
IBM AppConnect [y/N]
Red Hat ODF [y/N] n


6) Configure Authentication
🔐 IBM Entitlement Key >  ************************************************************************************************************************************************************************************************


7) Review Settings

    Settings
    Mirror Mode ......................... direct
    Working Directory ................... /mnt/registry
    Target Registry ..................... avregistry1.fyre.ibm.com:5000

    IBM Operator Catalog
    Catalog Version ..................... v9-250902-amd64
    MAS Update Channel .................. 9.1.x

    Content Selection (Core Platform)
    IBM Maximo Operator Catalog ......... Mirror
    IBM Maximo Application Suite Core ... Mirror

    Content Selection (Applications)
    IBM Maximo Assist ................... Skip
    IBM Maximo IoT ...................... Skip
    IBM Maximo Manage ................... Mirror
    + IBM Maximo IT ..................... Skip
    IBM Maximo Monitor .................. Skip
    IBM Maximo Predict .................. Skip
    IBM Maximo Optimizer ................ Skip
    IBM Maximo Visual Inspection ........ Skip
    IBM Maximo Facilities ............... Skip

    Content Selection (Cloud Pak for Data)
    IBM Cloud Pak for Data (CP4D) ....... Skip
    IBM Watson Studio ................... Skip
    IBM Watson Machine Learning ......... Skip
    IBM Analytics Engine (Spark)......... Skip
    IBM Cognos Analytics ................ Skip

    Content Selection (Other Dependencies)
    IBM Cloud Pak Foundation Services ... Mirror
    IBM Suite License Service ........... Mirror
    IBM Truststore Manager .............. Mirror
    MongoDb Community Edition ........... Mirror
    + Version 4 ......................... Skip
    + Version 5 ......................... Skip
    + Version 6 ......................... Skip
    + Version 7 ......................... Skip
    IBM Db2 ............................. Mirror
    IBM AppConnect ...................... Skip
    RedHat ODF .......................... Skip

Proceed with these settings [y/N] y


8) Run Mirror Process
Mirroring IBM Maximo Application Suite Core ... /mnt/registry/logs/mirror-20250926-040328-core.log
[SKIPPED] IBM Maximo Assist
[SKIPPED] IBM Maximo IoT
Mirroring IBM Maximo Manage ... /mnt/registry/logs/mirror-20250926-040328-manage.log
[SKIPPED] IBM Maximo Monitor
[SKIPPED] IBM Maximo Predict
[SKIPPED] IBM Maximo Optimizer
[SKIPPED] IBM Maximo Visual Inspection
[SKIPPED] IBM Maximo Facilities
[SUCCESS] Selected Dependencies: /mnt/registry/logs/mirror-20250926-040328-dependencies.log
[ibmmas/cli:15.6.1]mascli$
```

3. When done, check the registry:

```
$ curl -u $name:$password -k https://avregistry1.fyre.ibm.com:5000/v2/_catalog | jq

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  3043  100  3043    0     0  12086      0 --:--:-- --:--:-- --:--:-- 12075
{
  "repositories": [
    "amq-streams/bridge-rhel9",
    "amq-streams/kafka-39-rhel9",
    "amq-streams/kafka-40-rhel9",
    "amq-streams/maven-builder-rhel9",
    "amq-streams/strimzi-operator-bundle",
    "amq-streams/strimzi-rhel9-operator",
    "brancz/kube-rbac-proxy",
    "cert-manager/cert-manager-istio-csr-rhel9",
    "cert-manager/cert-manager-operator-bundle",
    "cert-manager/cert-manager-operator-rhel9",
    "cert-manager/jetstack-cert-manager-acmesolver-rhel9",
    "cert-manager/jetstack-cert-manager-rhel9",
    "community-operator-pipeline-prod/grafana-operator",
    "community-operator-pipeline-prod/opentelemetry-operator",
    "community-operator-pipeline-prod/strimzi-kafka-operator",
    "cp/cpd/edb-postgres-license-provider",
    "cp/cpd/norootsquash",
    "cp/manage/bdi",
    "cp/manage/extension-acm",
    "cp/manage/extension-aip",
    "cp/manage/extension-aviation",
    "cp/manage/extension-civil",
    "cp/manage/extension-envizi",
    "cp/manage/extension-health",
    "cp/manage/extension-hse",
    "cp/manage/extension-nuclear",
    "cp/manage/extension-oilandgas",
    "cp/manage/extension-oracleadapter",
    "cp/manage/extension-sapadapter",
    "cp/manage/extension-serviceprovider",
    "cp/manage/extension-spatial",
    "cp/manage/extension-strategize",
    "cp/manage/extension-transportation",
    "cp/manage/extension-tririga",
    "cp/manage/extension-utilities",
    "cp/manage/extension-workday",
    "cp/manage/health-aio",
    "cp/manage/health-utilities-accelerator",
    "cp/manage/healthext-model-engine",
    "cp/manage/ibm-mas-healthext-ws",
    "cp/manage/ibm-mas-imagestitching",
    "cp/manage/ibm-mas-manage-acc",
    "cp/manage/ibm-mas-manage-appstatus",
    "cp/manage/ibm-mas-manage-bdi",
    "cp/manage/ibm-mas-manage-primary-entity",
    "cp/manage/ibm-mas-manage-ws",
    "cp/manage/ibm-mas-slackproxy",
    "cp/manage/icdslack",
    "cp/manage/image-stitching",
    "cp/manage/manage-groupsyncagent",
    "cp/manage/manage-usersyncagent",
    "cp/manage/manageadmin",
    "cp/manage/manageadminfoundation",
    "cp/manage/maxloader",
    "cp/manage/monitoragent",
    "cp/manage/ubi-wlp-jms-manage",
    "cp/manage/ubi-wlp-manage",
    "cp/manage/ubi-wlp-manage-foundation",
    "cp/mas/accapppoints",
    "cp/mas/admin-dashboard",
    "cp/mas/adoptionusage-metering",
    "cp/mas/adoptionusage-reporter",
    "cp/mas/adoptionusageapi",
    "cp/mas/catalogapi",
    "cp/mas/catalogmgr",
    "cp/mas/coreapi",
    "cp/mas/coreidp",
    "cp/mas/coreidp-login",
    "cp/mas/datamodel-migration",
    "cp/mas/graphite-configuration",
    "cp/mas/groupsync-coordinator",
    "cp/mas/homepage",
    "cp/mas/ibm-mas-entitymgr",
    "cp/mas/ibm-mas-suite",
    "cp/mas/importuser",
    "cp/mas/internalapi",
    "cp/mas/kubectl",
    "cp/mas/licensing-mediator",
    "cp/mas/licensing-sync",
    "cp/mas/ltpakeys-generator",
    "cp/mas/milestonesapi",
    "cp/mas/mobileapi",
    "cp/mas/monagent-mas",
    "cp/mas/navigator",
    "cp/mas/oidcclient-reg",
    "cp/mas/push-notification-service",
    "cp/mas/scimsync",
    "cp/mas/scimsync-agent",
    "cp/mas/sendmailapi",
    "cp/mas/sim-user-data-service",
    "cp/mas/usersync-coordinator",
    "cp/mas/workspace-coordinator",
    "cpopen/common-service-operator",
    "cpopen/cpfs/common-web-ui",
    "cpopen/cpfs/cpfs-oadp-plugins",
    "cpopen/cpfs/cpfs-utils",
    "cpopen/cpfs/iam-custom-hostname",
    "cpopen/cpfs/ibm-events-kafka-3.6.1",
    "cpopen/cpfs/ibm-events-kafka-3.8.0",
    "cpopen/cpfs/icp-identity-manager"
  ]
}
```

*__Next: [Mirroring Red Hat images](./masredhatimages.md)__*

*__Back to [README](../README.md)__*