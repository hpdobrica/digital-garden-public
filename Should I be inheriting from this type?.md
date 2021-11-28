---
title : Should I be inheriting from this type?
notetype : feed
date : 28-11-2021
---

[[Composition Over Inheritance]] as [[OOP]] principle doesn't have much value if we don't invest time to think about the cases when [[Inheritance]] should be favored over Composition.

If a class would expose all public methods of another class, it's a good use case for inheritance. If anywhere you use `Animal` in your application, you could just as well use `Dog` without any issues, `Dog inherits Animal` is a good idea. See [[Liskov Substitution Principle]].

If a class wants only part of the behaviour exposed by another class, you'd be much better off with Composition.

-----

Status: #🌱 


