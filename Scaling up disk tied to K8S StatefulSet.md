---
title: Scaling up disk tied to K8S StatefulSet
notetype: feed
date: 04-02-2025
---

The procedure below can be used in case Storage Class used supports volume expansion, which you can check with:
```sh
k get storageclass $STORAGE_CLASS_NAME -o yaml | grep allowVolumeExpansion
```

If above command returns `true`, you can proceed with editing each PVC and increasing the amount of storage under `spec.resources.resources.requests.storage`.

Once this is done, verify that every pod has updated the amount of storage it has by running `df -h`. If some pod did not automatically pick up the change, restart it.

Next thing we need to do is change the [[K8S StatefulSet]] and update the amount of storage it requests inside its `volumeClaimTemplate` to the same number we added to our PVCs. To do this we need to:
- `k get sts $STS_NAME -o yaml > /tmp/my-sts.yaml`
- update the `volumeClaimTemplate` inside `/tmp/my-sts.yaml`
- delete the existing sts without deleting its pods by running `k delete sts $STS_NAME --cascade=orphan`
	- **don't forget `--cascade=orphan` or your day will be ruined**
- recreate the sts with new volume size by running `k apply -f /tmp/my-sts.yaml`

-----

Status: #💡 
