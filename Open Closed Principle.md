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


-----

Status: #💡 

References:
- [[Video - SOLID Go Design]] ([Source](https://www.youtube.com/watch?v=zzAdEt3xZ1M&ab_channel=GopherConUK))
- [[Blog - Golang SOLID - Open Closed Principle]]
