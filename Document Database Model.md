---
title: Document Database Model
notetype: feed
date: 09-03-2025
---

Document [[Database Model]] is an approach to structuring and managing data in [[Database]]s.

Data is stored as **documents** (usually JSON or BSON) inside **collections**. Documents can be **self-contained** (denormalized), reducing the need for joins.

The main arguments in favor of the document data model versus the [[Relational Database Model]] are **schema flexibility**, **better performance** due to locality (data you access together is often stored together), and that for some applications it is **closer to the data structures used by the application**. 

The locality advantage only applies if you need large parts of the document at the same time. The database typically needs to load the entire document, even if you access only a small portion of it. On updates to a document, the entire document usually needs to be rewritten. It is recommended that you **keep documents small** and **avoid writes that increase the size of a document** (as they might have to be moved).

If the data in your application has a **document-like structure** (i.e., a tree of one-to-many relationships, where typically the entire tree is loaded at once), then it’s probably a good idea to use a document model - However, if your application does use many-to-many relationships, the document model becomes less appealing.

# "Schemaless" database

Document databases are sometimes called schemaless, but that’s misleading, as the code that reads the data usually assumes some kind of structure — i.e., there is an implicit schema, but it is not enforced by the database.

A more accurate term is **schema-on-read** (the structure of the data is implicit, and only interpreted when the data is read), in contrast with **schema-on-write** (the traditional approach of [[Relational Database Model]], where the schema is explicit and the database ensures all written data conforms to it)

Schema-on-read is useful if there are many different types of objects, and it is not practical to put each type of object in its own table, or if the structure of the data is determined by external systems over which you have no control and which may change at any time.



-----

Status: #📥

References:
-  [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))
