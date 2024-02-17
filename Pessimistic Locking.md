---
title : Pessimistic Locking
notetype : feed
date : 10-08-2022
---

Pessimistic Locking in [[Public/Database]] systems is a locking mechanism that relies on exclusive locks to ensure two transactions don't update rows at the same time.

For example:
- user A fetches account data which says `amount: 100` and acquires `shared read lock` on this row
- user B fetches account data which says `amount: 100` and acquires `shared read lock` on this row
- if any of them wants to change the row, they need to acquire `exclusive write lock`
- `exclusive write lock` can only be obtained by either of them once the other one gives up their `shared read lock`

This approach guarantees better integrity than [[Public/Optimistic Locking]], but as you can imagine from the example above, it's pretty easy to create a [[Deadlock]] in the application code if you are not careful.

[[Public/Optimistic Locking]] is a better alternative in cases when the cost of retrying the transaction is not too high - if this is the case, Pessimistic Locking should be preferred.




-----

Status: #🌱 

References:
- https://vladmihalcea.com/optimistic-vs-pessimistic-locking/
