---
title : Liskov Substitution Principle
notetype : feed
date : 28-11-2021
---
Liskov Substitution Principle is the third of the [[Software Design]] [[SOLID Principles]] in [[OOP]]. It states this:

If `S` is a subtype of `T`, then objects of type `T` may be replaced with objects of type `S` without breaking the program.1

Or in plain english - if we have a class `Animal` and a class `Dog`, `Dog` should inherit from `Animal` only if we could replace **any instance** of `Animal` with an instance of `Dog` without breaking our code.

To do this, we need to make sure we follow a couple of guidelines when overriding `Dog`'s methods':
- Dog can't change any return type of any inherited method (covariance)
- Dog can't change any input types of any inherited method (contravariance)
- Dog can't have any additional input checks on inherited methods (cant strengthen preconditions)
- Dog can't have any additional output checks on inherited methods (cant weaken postconditions)
- Dog can't throw any new exceptions in inherited methods

If our `Dog` can't fulfil these rules, we should probably not make it inherit from `Animal`. See [[Public/Should I be inheriting from this type|Should I be inheriting from this type]].

-----

Status: #🌲 

References:
- [[Video - Liskov Substitution Principle Explained]] - [Youtube](https://www.youtube.com/watch?v=-3UXq2krhyw)
- [Wikipedia](https://en.wikipedia.org/wiki/Liskov_substitution_principle)