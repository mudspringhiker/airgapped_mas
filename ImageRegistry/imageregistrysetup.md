# Setting up the image registry

- Provisioned a RHEL 8.10 vm in Fyre
- Expanded the disk up to 1000G

```
[root@avregistry1 ~]# lsblk
NAME          MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
vda           252:0    0  1000G  0 disk
├─vda1        252:1    0     1G  0 part /boot
└─vda2        252:2    0 930.3G  0 part
  ├─rhel-root 253:0    0 914.3G  0 lvm  /
  └─rhel-swap 253:1    0    16G  0 lvm  [SWAP]
```

- No need to partition the disk, it turns out
- Copied the following files in the vm (using sftp):
    - registry_creation.sh
    - pull-secret
    - openshift-client tar file
```
[root@avregistry1 ~]# ls -alt
total 72592
dr-xr-xr-x. 18 root root      283 Sep 25 19:01 ..
dr-xr-x---.  3 root root     4096 Sep 25 19:01 .
-rw-------   1 root root      146 Sep 25 13:30 .bash_history
-rwxr-xr-x   1 root root     2471 Sep 25 12:14 registry_creation.sh
-rw-r--r--   1 root root     2783 Sep 25 12:12 pull-secret.dms
-rw-r--r--   1 root root 74268999 Sep 25 12:11 openshift-client-linux-amd64-rhel8.tar.gz
drwx------.  2 root root       85 Sep 15 11:37 .ssh
-rw-------   1 root root       58 May 15 07:52 .lesshst
-rw-r--r--.  1 root root      242 Feb 18  2025 .wget-hsts
-rw-r--r--   1 root root    12164 Feb 10  2025 katello-ca-consumer-latest.noarch.rpm
-rw-------.  1 root root     1465 May 28  2024 anaconda-ks.cfg
-rw-r--r--.  1 root root       18 Aug 12  2018 .bash_logout
-rw-r--r--.  1 root root      176 Aug 12  2018 .bash_profile
-rw-r--r--.  1 root root      176 Aug 12  2018 .bashrc
-rw-r--r--.  1 root root      100 Aug 12  2018 .cshrc
-rw-r--r--.  1 root root      129 Aug 12  2018 .tcshrc
```