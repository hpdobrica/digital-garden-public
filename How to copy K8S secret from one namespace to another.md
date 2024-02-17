---
title: How to copy K8S secret from one namespace to another
notetype: feed
date: 05-12-2023
---

[[Public/K8S Secret]]s can't be accessed across different environments. If you want to use an existing secret in another environment, you'll have to copy it there. To copy a secret from one namespace to another, you can use this simple script:

{% raw %}
```bash
SECRET_NAME=$1
SOURCE_NS=$2
DESTINATION_NS=$3

kubectl get secret $SECRET_NAME --namespace=$SOURCE_NS -o yaml | sed "s/namespace: .*/namespace: $DESTINATION_NS/" | kubectl -n $DESTINATION_NS apply -f -

```
{% endraw %}

-----

Status: #📥

References:
- 
