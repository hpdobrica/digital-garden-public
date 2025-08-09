---
title : CORS
notetype : feed
date : 25-02-2022
---

CORS (Cross-Origin Resource Sharing) is a mechanism that allows the server to dictate from which other origins a browser should be allowed to load its resources.

For example, if i serve a website from `my-domain.com`, and use [[Javascript]] to try to fetch a resource like `someone-elses-domain.com/cool.json`, `someone-elses-domain.com` would need to use a CORS header to explicitly allow me to request this from a domain other than its own.

In the simplest case, your browser script makes a GET request for a resource from a server in another domain. Depending on the CORS configuration of that server, if the server thinks that your domain is authorized to submit GET requests, the cross-origin server responds by returning the requested resource.

If either the requesting domain or the verb of HTTP request is not authorized, the request is denied. 

However in order to stop you from making unneeded, unallowed requests, CORS makes it possible to preflight the request before actually submitting it. A preflight request is an `OPTIONS` verb request that a browser makes before your request to get the CORS configuration of the targeted server and check if making the actual request is possible

From here, depending on the received CORS configuration, the client either sends the original request or raises a CORS error.

-----

Status: #💡 

References:
- [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
