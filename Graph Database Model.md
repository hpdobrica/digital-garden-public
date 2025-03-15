---
title : Graph Database Model
notetype : feed
date : 12-03-2025
---

Many-to-many relationships are what gives advantage to [[Relational Database Model]] over [[Document Database Model]], but in cases when we have a lot of complex many-to-many relationships, it is good to start thinking about how to model our data as a graph.

Graphs are good for evolvability: as you add features to your application, a graph can easily be extended to accommodate changes in your application’s data structures.

There are several similar ways of structuring and querying data in graphs, like Property Graph Model and Triple-Store Model.

## Property Graph Model

implemented by [[Neo4j]], Titan, InfiniteGraph...

You can think of a graph store as consisting of two relational tables, one for vertices and one for edges.

Each vertex is given a symbolic name like USA or Idaho. Other parts of the query can use those names to create edges between the vertices, using an arrow notation: `(Idaho) -[: WITHIN]- > (USA)` creates an edge labeled WITHIN, with Idaho as the tail node and USA as the head node.

## Triple-Store Model

implemented by Datomic, AllegroGraph...

The triple-store model is mostly equivalent to the property graph model, using different words to describe the same ideas. 

The data is stored as tripets containing subject, predicate a

-----

Status: #📥

References:
- [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))
