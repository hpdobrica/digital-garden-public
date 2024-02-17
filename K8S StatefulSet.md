---
title : K8S StatefulSet
notetype : feed
date : 21-01-2023
---

StatefulSet is an object that manages a set of [[Public/K8S Pod]]s and provides guarantees on their ordering and uniqueness.

It is pretty similar to [[K8S Deployment]], but has a few important differences which make it a much better candidate for managing stateful applications:
- instead of pods getting a random name suffix, StatefulSet always gives the same suffix to the pod it creates
	- for example, first pod created by StatefulSet called `test` will always be called `test-0`, second one `test-1` and so on
- since pods maintain their identity, StatefulSets can reuse existing volumes, so that if `test-1` pod is recreated, new `test-1` pod will be able to keep using the same volume as the old one
- if we delete a pod of a StatefulSet, its PVC is not deleted by default so it can be reused by a new pod (this can be overridden by changing `persistentVolumeClaimRetentionPolicy`)
- they are rolled out and rolled back in order (assuming default pod management policy `OrderedReady` is used):
	- when creating pods, StatefulSet will ensure the pod `test-0` is ready before moving on to provision `test-1`
	- when destroying pods, StatefulSet will ensure the pod with the highest index is destroyed first, before moving on to the pod with the next lowest index
	- when updating pods, StatefulSet will first recreate the pod with the highest index, and once it's ready it will move on to the pod with the next highest index (assuming default update strategy `RollingUpdate` is used)
- StatefulSets need a [[Public/Headless Service]] which needs to be manually created

-----

Status: #💡 

References:
- [K8S Docs](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/)