---
title : Headless Service
notetype : feed
date : 31-10-2022
---

A [[Kubernetes Service]] will expose an IP address, and when you reach it, it will forward your request to one of the underlying pods. This is good if you want to connect to one pod, but what if you want to connect to all of them?

This is where the concept of a headless service comes into play - when you do a DNS lookup of a headless service, instead of getting one IP address in an A record, you'd get multiple A records, each holding an IP address of the underlying pod. 

In Kubernetes, you can achieve this by setting service's `clusterIP` spec field to `None`.

There is an option to also publish the addresses of pods which are not ready: `spec.publishNotReadyAddresses: true`

-----

Status: #💡 


