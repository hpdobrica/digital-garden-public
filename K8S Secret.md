---
title : K8S Secret
notetype : feed
date : 08-11-2021
---

Secrets are [[K8S Object]]s which are used to store sensitive information you can't otherwise put into a Pod spec or a [[K8S ConfigMap]].

Secrets are very similar to ConfigMaps, the biggest difference being that they are designed to be used for confidential data.

Secret can come in one of several types, depending on it's usage and the type of data it holds (e.g. Opaque, docker config, basic auth, ssh auth..)

Secrets are stored unencrypted in [[etcd cluster]] by default - See [[K8S Encryption]] . Anyone who can create a pod in a namespace can read secrets in that namespace - you need to configure [[K8S RBAC]] rules to counter this.

-----

Status: #💡 

References:
- https://kubernetes.io/docs/concepts/configuration/secret/
