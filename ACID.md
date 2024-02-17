---
title : ACID Transactions
notetype : feed
date : 10-08-2022
---

ACID is a set of properties of [[Public/Database]] systems that talks about how a database transaction should behave in order for it to be considered reliable. It stands for:

- `A`tomicity
- `C`onsistency
- `I`solation
- `D`urability

## Atomicity

Atomicity says that either the transaction is executed in its entirety, or the database must be in an untouched state if the transaction has failed - nothing in between.

Imagine having a database transaction consisting of two queries:
- one to deduct money from account A
- one to add money to the account B

It would be pretty inconvenient for us to be able to mistakenly deduct money from A without actually adding it to B. Atomicity just says that this database guarantees that either both queries will be completed without issues, or the database will be returned to the state before this transaction was issued.

## Consistency

Consistency just says that when we write into a database, any constraints we have on the data must be followed, and any cascades or triggers executed - otherwise the transaction will fail. At the end of the transaction, data in our database must be consistent.


## Isolation

Isolation states that if we have two concurrently-running transactions, database guarantees us that neither of them will be influenced by one another - they will both be executed in total isolation.

Any concurrent transactions touching the same data must be resolved in a sequential-like manner. If this is not possible, databases resolve this either through [[Public/Optimistic Locking]] or [[Public/Pessimistic Locking]].

## Durability

Durability states that the moment transaction is commited, it's submitted to the persistent storage. If a crash occurs a mere moment after the transaction was successful, we are guaranteed that our transaction is not lost.



-----

Status: #🌱 

References:
- 
