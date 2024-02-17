---
title : K8S Encryption
notetype : feed
date : 13-11-2021
---

In order to enable encryption of data stored in [[Public/etcd cluster]], [[Public/K8S Apiserver]] needs to be configured with the `--encryption-provider-config` flag:

First, create a file `encryption-config.yaml`:

```yaml
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
    - secrets
    providers:
    - aescbc:
        keys:
        - name: key1
          secret: some-example-key
    - identity: {}
```

Next, make sure that apiserver pod can access the file. For example, create `/etc/kubernetes/encryption` directory and mount it to the apiserver, and then set the flag like so: `--encryption-provider-config=/etc/kubernetes/encryption/encryption-config.yaml`.


-----

Status: #💡 

References:
- https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/
- 