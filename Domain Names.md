---
title : Domain Names
notetype : feed
date : 31-10-2021
---

While our local network hosts can be referenced with names such as `db`, on the internet, hosts use a special Domain Name format: `www.google.com`.

The purpose of this format is to group similar things together. The last portion of the domain (`.com`) is called the top-level domain. `google` is the domain name, while `www` is the subdomain - of which google has many (`maps`, `workspace`, `photos`).

When you try to reach `maps.google.com` in your organization, your request first hits your organization's internal [[DNS]] Server. It doesn't know who `maps` nor `google` is, so it forwards your request to the internet.

From here multiple DNS Servers help resolve your request:

-   Root DNS Server looks at your request and forwards it to the DNS Server resolving `.com` domains
    
-   `.com` DNS Server looks at your request and forwards you to `google`
    
-   Google's DNS Server provides you with the ip address of the server serving the `maps` application
    
-   In order to speed up the resolution in the future, your organization's DNS Server can chose to cache this record for a period of time (few secs - few mins).
    

So if you have a domain dobrica.sh, and you want to resolve db.dobrica.sh to your db - if you wrote a record like this, you wouldn't be able to reach your db in local network as just `db` anymore. How do you say "when i say `db`, i mean `db.dobrica.sh`"? You can add another line to your `/etc/resolv.conf` file: `search dobrica.sh`. Next time you try to ping `db`, you will see it tries to reach `db.dobrica.sh`.