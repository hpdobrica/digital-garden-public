---
title: Database Model
notetype: feed
date: 12-03-2025
---
Database models are different approaches to structuring and managing data in [[Database]]s.

It’s not possible to say in general which data model leads to simpler application code; it depends on the kinds of relationships that exist between data items:
- If the data in your application has a document-like structure (i.e., a tree of one-to-many relationships, where typically the entire tree is loaded at once), then it’s probably a good idea to use a [[Document Database Model]].
- If your application does use many-to-many relationships, the document model becomes less appealing and [[Relational Database Model]] might be a better fit.
- For highly interconnected data, the document model is awkward, the relational model is acceptable, and [[Graph Database Model]]s are the most natural.
- There are also use-cases like genome sequencing where special implementations are needed (e.g. GenBank)

See also:
- [[Hierarchical Database Model]]
- [[Network Database Model]]

-----

Status: #📥

References:
-  [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))
