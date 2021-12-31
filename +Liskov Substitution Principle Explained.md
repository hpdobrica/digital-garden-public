---
title : +Liskov Substitution Principle Explained
notetype : unfeed
date : 28-11-2021
---

- [[Liskov Substitution Principle]] states: If `S` is a subtype of `T`, then objects of type `T` may be replaced with objects of type `S` without breaking the program.
- lets look at an example program
	- Eployee class has `firstName`, `lastName`, `manager`, `salary`, `AssignManager()`, `CalculatePerHourRate()`
	- Manager inherits from Employee and overrides `CalculatePerHourRate()`, and has additional method `GeneratePerformanceReview()`
	- CEO also inherits from Employee, overrides `CalculatePerHourRate()`, `AssignManager()` which just throws an exception since CEO has no manager,  `GeneratePerformanceReview()` and has `FireSomeone()`
	- If we create a new employee, set its name, set its manager and calculate their salary 
- this design validates LSP
	- if we replace Employee with Manager the program still executes
	- if we replace Eployee with CEO we will get an error stating that "CEO has no manager"
- covariance and contravariance
	- covariance talks about return type of a method (it cant change)
	- contravariance talks about input types of a method (it cant change)
- preconditions and postconditions
	- you cannot strengthen preconditions (cant add additional input checks)
	- you cannot weaken postconditions (cant remove output checks)
- you cannot return new exceptions
- solution to the problem above
	- create interfaces IEmployee IManager IManaged
	- create BaseEmployee class which implements IEmployee
	- create Employee class which inherits from BaseEmployee and implements IManaged
	- create Manager class which inherits from Employee and implements IManager
	- create CEO class which inherits from BaseEmployee and implements IManager


-----

Status: #📥/📹/✅

References:
- https://www.youtube.com/watch?v=-3UXq2krhyw&ab_channel=IAmTimCorey
