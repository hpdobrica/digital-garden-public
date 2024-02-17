---
title : DNS Resolution
notetype : feed
date : 02-11-2021
---

[[DNS]] Resolution is a process in which [[Domain Name]] are converted to IP addresses of the hosts they point to.

The process of resolution is handled by multiple DNS servers which forward the requests to each other in order to find the server with the actual IP address. In the example of `maps.google.com`:
- Your local machine doesn't know what `maps.google.com` is, so it forwards the request to the DNS Servers on the internet
- Root DNS Server looks at your request and forwards it to the [[DNS Server]] resolving `.com` domains
- `.com` DNS Server looks at your request and forwards you to `google`'s DNS
- Google's DNS Server provides you with the ip address of the server serving the `maps` application
- In order to speed up the resolution in the future, your machine can chose to cache this record for a period of time (few secs - few mins).
    

-----

Status: #🌲 

References:
- 
