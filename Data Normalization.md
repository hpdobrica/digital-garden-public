---
title : Data Normalization
notetype : feed
date : 09-03-2025
---
In [[Relational Database Model|Relational Databases]], the data is often normalized to reduce redundancy and maintain consistency.

Let's say you have a table with student data. If you are storing all their details in the database directly as text(e.g. school name), you are duplicating the this data for every student who is going to this school. If the name of the school changes, we'd have to update many records for all the students that have school name written in their rows. 

The advantage of using an unique ID for such entities is that because it has no meaning to humans, it never needs to change: the ID can remain the same, even if the information it identifies changes. Anything that is meaningful to humans may need to change sometime in the future— and if that information is duplicated, all the redundant copies need to be updated. That incurs write overheads, and risks inconsistencies (where some copies of the information are updated but others aren’t). Removing such duplication is the key idea behind normalization in databases.

-----

Status: #📥

References:
-  [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))
