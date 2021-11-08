---
title : Docker Networking
notetype : feed
date : 03-11-2021
---

When running a [[Docke]] container, there are several networking options to chose from:

## None
Runs a container in a completely isolated network. Container can't reach anything outside of it, and nothing can reach the container.

```bash
docker run --network none nginx
```

## Host
Host option attaches the container to the host network. This approach provides no network isolation between the container and the host. In other words, if you create a container that listens on port 8080, there is no need to do any additional port mapping, the container will be available on localhost:8080

```bash
docker run --network host nginx
```

## Bridge

This is the most often used networking option. In this case, an internal private network is created for the host and the containers to attach to. The network has IP address `172.17.0.0` by default, and each container connected to this network gets their own IP address on it, e.g. `172.17.0.2` , `172.17.0.3`...

See [[Docker Bridge Network]] for more details on how this works.

-----

Status: #🌲 


