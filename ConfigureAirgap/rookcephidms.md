# New IDMS for rook

apiVersion: config.openshift.io/v1
kind: ImageDigestMirrorSet
metadata:
  name: rook-ceph-mirrors
spec:
  imageDigestMirrors:
    - mirrorSourcePolicy: NeverContactSource
      mirrors:
        - "avregistry1.fyre.ibm.com:5000/ceph"
      source: quay.io/ceph
    - mirrorSourcePolicy: NeverContactSource
      mirrors:
        - "avregistry1.fyre.ibm.com:5000/cephcsi"
      source: quay.io/cephcsi

Having this did not automatically resolve the pending pods. I hacked the pods such that the image is pointing to the on in the private registry