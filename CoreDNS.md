---
title : CoreDNS
notetype : feed
date : 03-11-2021
---

CoreDNS is one of many [[DNS Server]] solutions, which is particuarily interesting because it's used for [[DNS Resolution in Kubernetes]]. Most of its functionality is implemented through plugins, so it's very flexible and extensible by nature.

Let's see how we can configure a host to be a DNS Server.

To start, you can download the executable and execute it:

```bash
wget https://github.com/coredns/coredns/releases/download/v1.8.4/coredns_1.8.4_linux_amd64.tgz 
#> coredns_1.8.4_linux_amd64.tgz 

tar -xzvf coredns_1.8.4_linux_amd64.tgz 
#> coredns 

./coredns 
#> .:53 
#> [INFO] CoreDNS-1.8.4 
#> [INFO] linux/amd64, go1.12 
#> ...
```

To configure the CoreDNS to have names and addresses that we want, we use `Corefile` - a file for configuring CoreDNS. In there we can set it to read our local `/etc/hosts` file like so:

```Corefile
cat >> Corefile 
{ 
	hosts /etc/hosts 
}
```

The `hosts` section that we specified in Corefile is actually a [plugin](https://coredns.io/plugins/hosts/).

-----

Status: #💡 

References:
- [CoreDNS Configuration](https://coredns.io/manual/toc/#configuration)
- https://coredns.io/plugins/hosts/
