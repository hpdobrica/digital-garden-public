---
title : Optimistic Locking
notetype : feed
date : 10-08-2022
---

Optimistic Locking in [[Database]] systems is a locking mechanism that relies on data versions to stop updates based on stale data.

For example:
- user A fetches account data which says `amount: 100, version: 1`
- user B fetches the same row, getting `amount: 100, version: 1`
- user B updates the row remove 100, succeeds and updates the record to `amount: 0, version: 2`
- user A tries to remove 10 more, but their update fails because they were trying to update based on version 1, which is not the current version anymore

Optimistic locking is non-blocking - if the "locked" key was changed, the transaction will fail, will be reverted ([[ACID]]) and retried.

If the cost of retrying a transaction is too high, [[Pessimistic Locking]] should be preferred.

-----

Status: #🌱 

References:
- https://vladmihalcea.com/optimistic-vs-pessimistic-locking/
