---
title : Blog - Practical SOLID in Golang - Open Closed Principle
notetype : unfeed
date : 07-08-2022
---

------

Source: [Practical SOLID in Golang: Open/Closed Principle](https://levelup.gitconnected.com/practical-solid-in-golang-open-closed-principle-1dd361565452)

Status: #🛈/📰/✅ 


-----

- "Software entities should be open for extension, but closed for modification"
- in other words, you should be able to extend the behavior of a system, without having to modify the system
- bad example:
	- authorization module (separate from authentication)
	- it extracts permissions from req in a different way based on the auth method (we have a switch statement basically)
	- this implies that
		- extending authentication module with new auth method also forces you to modify authorization module
		- the more auth flows you have, the more your authorization logic grows
		- authorization becomes harder to test because you have unrelated logic
- better example:
	- instead of doing above, we should provide something that would allow our code to be extended from the outside
	- we can achieve open/closed principe with different implementations for the same interface - polymorphism
	- permission checker should have an array of permission providers
	- this allows us to implement its own logic separately, to extend the authorization module, and to not have to modify it once authenitcation changes
	- instead of having array of providers, we can provide desired provider as argument