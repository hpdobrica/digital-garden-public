---
title : Prometheus Storage
notetype : feed
date : 28-06-2022
---

Prometheus stores data locally on the disk in a custom [[Public/Database]]. It doesn't support any form of clustering by itself, in an attempt to make running Prometheus a simple task. 

This means that you are limited by the storage space on your machine. This also means that long-term storage is quite hard to pull off with Prometheus on its own.

Luckily, Prometheus exposes remote read and write APIs, which allows other software to seamlessly implement any missing functionality. This approach allows PromQL queries to be transparently run against both local and remote data.

A piece of software that exploits this functionality and can be used for longer term storage of metrics is Thanos.

-----

Status: #🌱 

References:
- [[Private/Book - Prometheus Up And Running]] ([Source](https://www.oreilly.com/library/view/prometheus-up/9781492034131/))
