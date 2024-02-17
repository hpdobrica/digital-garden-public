---
title : How to quickly read K8S Secret Value
notetype : feed
date : 18-01-2022
---

To get the value of a [[Public/K8S Secret]], all you need to know is the secret name and the name of the key that you want to read.

What I would normally do before is:
- `kubectl get secret mysecret -o yaml`
- copy the (often very long) base64 string under the key i wish to read
- `echo "million_character_base64_string_here" | base64 -d`

While this works, there is an easier way:

{% raw %}
```bash
kubectl get secret $SECRET_NAME -o 'go-template={{ index .data "$KEY_NAME" }}' | base64 -d

```
{% endraw %}

Neat - now it's a one-liner and i don't have to copy anything!

-----

Status: #🌲 

