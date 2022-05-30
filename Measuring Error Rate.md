---
title : Measuring Error Rate
notetype : feed
date : 29-05-2022
---

Errors show us a rate of failed requests, and are one of [[The Four Golden Signals of Monitoring]].  

Error rates can look at requests that failed:
- directly (5XX errors) – fetched at load balancer level is an easy way to track this globally. See [[Where to Collect Metrics#Infrastructure-exported Metrics]]
- indirectly (2XX code but wrong response) – which is hard to track, see [[Where to Collect Metrics#Synthetic Clients]]
- by policy (e.g., any request served over 1s could be treated as an error)

 

-----

Status: #🌱 

References:
- [[Book - Why Buddhism Is True]]
