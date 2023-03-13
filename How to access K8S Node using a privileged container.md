If you have a [[K8S Pod]] with a privileged container running in [[Kubernetes]] cluster, you can use it to gain access (like ssh) to the underlying [[K8S Node]] it's running on by using `nsenter`.

{% raw %}
```bash
NAMESPACE=$1
PRIVILEGED_POD_NAME=$2

kubectl exec -n $NAMESPACE -ti $PRIVILEGED_POD_NAME -- bash -c "nsenter --mount=/proc/1/ns/mnt -- /bin/bash"
```
{% endraw %}

To see if a container is privileged, look for privileged flag within its security context:
```bash
kubectl get pod $POD_NAME -o yaml | grep "privileged: true"
```


-----

Status: #🌲 