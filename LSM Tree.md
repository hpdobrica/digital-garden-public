---
title : LSM Tree
notetype : feed
date : 26-03-2025
---


Log-Structured Merge Tree is a [[Data Structure]] optimized for write-heavy workloads, used by storage engines like [[Cassandra]] and HBase. 

When a write comes in, we add it to an in-memory balanced tree data structure (for example, a red-black tree), often called a memtable.

When the memtable gets bigger than some threshold (e.g. a few megabytes), we write it to disk as an SSTable file, which is a immutable, write-once file containing sorted strings (SSTable == sorted string table).

When a read request comes in, we first check the memtable, then if we don't find the key, we move on to checking the youngest SSTable, and then proceed looking at next SSTable until we find the key.

To keep the process more efficient, in the background we will merge and compact (discard overwritten or deleted values) older SSTables into new ones, so there is less places to check.

Memtable and SSTable terms originate from [Google's Bigtable paper](https://static.googleusercontent.com/media/research.google.com/en//archive/bigtable-osdi06.pdf).

## Non-existent keys

LSM-Tree algorithm can be slow when looking up keys that don't exist in the database, as you have to check the memtable, 

-----

Status: #📥

References:
- [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))