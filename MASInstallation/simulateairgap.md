## Simulating airgap environment

Reference:

https://ibm-mas.github.io/support/airgap/40-airgap_simulateairgap/

```
export REGISTRY_PRIVATE_HOST=mlregistry1.fyre.ibm.com
export REGISTRY_PRIVATE_PORT=5000
export REGISTRY_PRIVATE_CA_FILE=/images/certs/domain.crt
export REGISTRY_USERNAME=admin
export REGISTRY_PASSWORD=redhat

ansible-playbook ansible-devops/playbooks/ocp_convert_to_disconnected.yml
```

Checking the /etc/hosts

get the source, encoded, for the etc file:

```
[root@avregistry1 ~]# echo "MTI3LjAuMC4xICAgbG9jYWxob3N0IGxvY2FsaG9zdC5sb2NhbGRvbWFpbiBsb2NhbGhvc3Q0IGxvY2FsaG9zdDQubG9jYWxkb21haW40Cjo6MSAgICAgICAgIGxvY2FsaG9zdCBsb2NhbGhvc3QubG9jYWxkb21haW4gbG9jYWxob3N0NiBsb2NhbGhvc3Q2LmxvY2FsZG9tYWluNgoxLjIuMy40ICAgICBxdWF5LmlvIHJlZ2lzdHJ5LnJlZGhhdC5pbyByZWdpc3RyeS5jb25uZWN0LnJlZGhhdC5jb20gZ2NyLmlvIG52Y3IuaW8gaWNyLmlvIGNwLmljci5pbyBkb2NrZXItbmEtcHVibGljLmFydGlmYWN0b3J5LnN3Zy1kZXZvcHMuY29tIGRvY2tlci1uYS1wcm94eS1zdmwuYXJ0aWZhY3Rvcnkuc3dnLWRldm9wcy5jb20gZG9ja2VyLW5hLXByb3h5LXJ0cC5hcnRpZmFjdG9yeS5zd2ctZGV2b3BzLmNvbQoxNzIuMzAuMzguMTc0IGltYWdlLXJlZ2lzdHJ5Lm9wZW5zaGlmdC1pbWFnZS1yZWdpc3RyeS5zdmMgaW1hZ2UtcmVnaXN0cnkub3BlbnNoaWZ0LWltYWdlLXJlZ2lzdHJ5LnN2Yy5jbHVzdGVyLmxvY2FsICMgb3BlbnNoaWZ0LWdlbmVyYXRlZC1ub2RlLXJlc29sdmVyCg==" | base64 -d
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
1.2.3.4     quay.io registry.redhat.io registry.connect.redhat.com gcr.io nvcr.io icr.io cp.icr.io docker-na-public.artifactory.swg-devops.com docker-na-proxy-svl.artifactory.swg-devops.com docker-na-proxy-rtp.artifactory.swg-devops.com
172.30.38.174 image-registry.openshift-image-registry.svc image-registry.openshift-image-registry.svc.cluster.local # openshift-generated-node-resolver
[root@avregistry1 ~]#
```


Then mas installation can be done.

