---
title : Database Index
notetype : feed
date : 15-03-2025
---

[[Database]] indexes are data structures that databases keep on the side to improve the speed of reading the primary data, at the cost of increased storage usage and speed of writes.

Indexes are derived from the primary data, and in many databases you can safely add and remove the without affecting the original data - just the speed of query execution.

Indexes optimize the speed of read queries, usually at the cost of speed of write queries. It's difficult to use a secondary data structure to improve write speeds, as the fastest way to write something is to write it only once - while indexes are active, in addition to writing the data to the database, you also need to update the indexes, which slows the writes down.

## In-memory Hash Maps 

Let's try making a simple key-value database that writes entries to a file (e.g. append-only file), and use in-memory hash map as an index. 

### Storing data on disk

Since whenever we update the file we are just appending data to it, and it's hard to remove obsolete data (e.g. old values) in place in this single file. Since the file is append-only, we remove keys by adding a new entry called a tombstone, which will tell the database the key is not "live" anymore.

In order to be able to clean up unneeded data (deleted keys, old values), we will split the data we write into segments: once we reach a certain threshold (e.g. 25mb written) we will close that file and start appending to a new file. In this scenario we call each file a segment.

Now that we have split the data into smaller segment, and the database is appending data only to the latest one, we can go through data in older segments and compact it (remove all entries for keys that have tombstones, drop old values, merge cleaned up segments). 

When we want to read the data, we'd have to search through the latest segment file from the beginning, which is slow and can be optimized by using in memory-hash map as index.

### Adding indexes

Whenever we write to disk, we also write the location of the key into an in-memory hash map that will help us locate this key without seeking through the whole file.

Whenever we open a new segment, we also open a new hash map index for this segment.

When compaction cleans up and merges the segments, it also modifies the hash maps to keep them up to date.

In order to find a value for a key, we would check the hash map of the latest segment, if we don't find it, we check the hash map of the next youngest segment, and so on. Since compaction process keeps the number of segments small, we don't have to check too many hash maps to find our value.

-----

Status: #📥

References:
-  [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))
