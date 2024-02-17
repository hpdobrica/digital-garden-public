---
title : Single Responsibility Principle
notetype : feed
date : 10-08-2022
---

Single Responsibility Principle (OCP) is the first of [[Public/SOLID Principles]] which states:

"**A class should have one, and only one, reason to change**"

In other words, if some code has to change, it should be for its own reasons, not as collateral damage of some other code change. To achieve this, we need to build modules/classes/functions/structs which have a single responsibility.

Sounds familiar? You might be thinking [[Public/Unix Philosophy]].

Instead of having a function that sends an email **and** writes it to a [[Public/Database]] ("and" here implying multiple responsibilities), we should preferably have two separate code structures, one for persisting to database, one for actually sending the email. Then, we can have a third component which utilizes the first two to send an email and write it into the database.

The example above might sound like we just moved the problem one abstraction up - we still have a module that's responsible for both sending a message and writing to database, right? Not quite - we have one module responsible only for **writing**, one responsible only for **sending**, and one responsible only for **delegating** work to underlying structures.

### Naming things

The name of the thing can have an impact on the responsibility of the code. Let's see a few examples with go package names:
- Let's say you name your package `server`. What is its responsibility? It's pretty clear, to serve something, right? But which protocol does it serve? See how go's package `net/http` did the right thing there?
- Packages like `util` and `common` are breeding grounds for multi-responsibility code

By naming our things properly, we ensure that we are sticking to the intended purpose of our code.



-----

Status: #💡 

References:
- [[Private/Video - SOLID Go Design]] ([Source](https://www.youtube.com/watch?v=zzAdEt3xZ1M&ab_channel=GopherConUK
- [Dave Cheney - SOLID Go Design](https://dave.cheney.net/2016/08/20/solid-go-design)

