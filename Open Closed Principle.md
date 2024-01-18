---
title : Open/Closed Principle
notetype : feed
date : 09-08-2022
---

Open/Closed Principle (OCP) is the second of [[SOLID Principles]] which states:

"**Software entities should be open for extension, but closed for modification**"

In a bit clearer wording, you should be able to extend the behavior of a system, without having to modify it.

A code example not following this principle might do something like this:
```go

type PermissionsChecker struct {
	// ...
}

func (p *PermissionsChecker) checkPermissions(req) {
	var permissions []string
	// ...

	if req.authenticationMethod == "token" {
		// ...extract permissions logic for token authentication...
	} else if req.authenticationMethod == "basic" {
		// ...extract permissions logic for basic authentication...
	}

	// ...check extracted permissions..
	// ...
}
```


In the example above, our authorization logic directly depends on our authentication implementation. If we were to add another authentication method, we'd have to modify the authorization as well. Because of this, we could say that this authorization is **closed for extension, and thus requires modification**.

A code example that follows the OCP better, could do something like this:

```go

type PermissionsProvider interface {
	Type() string
	GetPermissions(req) []string
}

type PermissionsChecker struct {
	providers []PermissionsProvider
	// ...
}

func (p *PermissionsChecker) checkPermissions(req) {
	var permissions []string
	// ...

	for _, provider := range c.providers {
		req.authenticationMethod != provider.Type() {
			continue
		}

		permissions = provider.GetPermissions(req)

	}

	// ...check extracted permissions..
	// ...
}

```

Here we define `PermissionsProvider` interface which allows us to extend our authorization logic without having to modify it. Each time you add new authentication method, you'd add another provider to the `PermissionsChecker`. Another option would be to pass the used `PermissionsProvider` as an argument to `checkPermissions` and avoid loop-through-all-providers shenanigans.

### Golang embedding

In golang, we can use embedding to open our code for extension, let's see a few examples:

```go
package main

type Cat struct {
        Legs int
}


func (c Cat) PrintLegs() {
        fmt.Printf("I have %d legs\n", c.Legs)
}

type OctoCat struct {
        Cat
}

func (o OctoCat) PrintLegs() {
        fmt.Printf("I have %d legs, even though I'm called OctoCat\n", o.Legs)
}

func main() {
		var cat Cat
		cat.Legs = 4;
        var octo OctoCat
        octo.Legs = 5;
        cat.PrintLegs()  // I have 4 legs
        octo.PrintLegs() // I have 5 legs, even though I'm called OctoCat
}
```

Here we embedded Cat into OctoCat, which allowed us to reuse all of it's fields and methods, but then we defined our own PrintLegs method to extend the existing functionality.


```go
package main

type Cat struct {
        Name string
}

func (c Cat) Legs() int { return 4 }

func (c Cat) PrintLegs() {
        fmt.Printf("I have %d legs\n", c.Legs())
}

type OctoCat struct {
        Cat
}

func (o OctoCat) Legs() int { return 5 }

func main() {
        var octo OctoCat
        fmt.Println(octo.Legs()) // 5
        octo.PrintLegs()         // I have 4 legs
}
```

In a similar example, if `Legs` are instead a method (and not a property) which we have overriden, while `PrintLegs` stays not-overriden, even though Octo's Legs() say 5, it's PrintLegs is called directly from `Cat`, which has no idea where it has been embedded into, and can only call it's own method Legs, thus saying that OctoCat has only 4 legs!



-----

Status: #💡 

References:
- [[Video - SOLID Go Design]] ([Source](https://www.youtube.com/watch?v=zzAdEt3xZ1M&ab_channel=GopherConUK))
- [[Blog - Golang SOLID - Open Closed Principle]] ([Source](https://levelup.gitconnected.com/practical-solid-in-golang-open-closed-principle-1dd361565452))
