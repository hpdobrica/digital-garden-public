---
title : Graph Database Model
notetype : feed
date : 12-03-2025
---

Many-to-many relationships are what gives advantage to [[Relational Database Model]] over [[Document Database Model]], but in cases when we have a lot of complex many-to-many relationships, it is good to start thinking about how to model our data as a graph.

There are several ways of structuring and querying data in graphs:

## Property Graph Model

implemented by [[Neo4j]], Titan, InfiniteGraph...

You can think of a graph store as consisting of two relational tables, one for vertices and one for edges

## Triple-Store Model

implemented by Datomic, AllegroGraph...

-----

Status: #📥

References:
- [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))
