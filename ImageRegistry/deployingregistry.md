## Deploying the registry

- Run [registry_creation](./registry_creation.sh) script
- Check the container using `podman ps`

```
[root@avregistry1 ~]# ./registry_creation.sh
Updating Subscription Management repositories.
Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)                                                                 71 kB/s | 4.1 kB     00:00
...
Installed products updated.
....
Complete!
Generating a RSA private key
..............................++++
.....................................................................................................................................++++
writing new private key to 'domain.key'
-----
Adding password for user admin
success
success
Trying to pull docker.io/library/registry:2...
Getting image source signatures
Copying blob 6d464ea18732 done   |
Copying blob 8e82f80af0de done   |
Copying blob 44cf07d57ee4 done   |
Copying blob bbbdd6c6894b done   |
Copying blob 3493bf46cdec done   |
Copying config 26b2eb0361 done   |
Writing manifest to image destination
501b98134b94bfb310f9671b79b962fdf9ef6c48d4d09215864705bafd4d8d2c

{"repositories":[]}


The script needs to return {"repositories":[]}, if it did everything worked.
[root@avregistry1 ~]# podman ps
CONTAINER ID  IMAGE                         COMMAND               CREATED         STATUS         PORTS                   NAMES
501b98134b94  docker.io/library/registry:2  /etc/docker/regis...  12 seconds ago  Up 11 seconds  0.0.0.0:5000->5000/tcp  registry
```

- Afterwards, `/Images` contains `auth`, `certs`, `data`: 

```
[root@avregistry1 ~]# tree /Images
/Images
├── auth
│   └── htpasswd
├── certs
│   ├── answerFile.txt
│   ├── domain.crt
│   └── domain.key
├── data
└── downloads
    ├── images
    ├── secrets
    └── tools
        └── start_registry.sh
```

`/Images/data` is where the registry data will live.

*__Next: [Mirroring MAS Images](../MirrorImages/masmirrorimages.md)__*

*__Back to [README](../README.md)__*