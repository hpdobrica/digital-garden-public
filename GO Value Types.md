---
title : GO Value Types
notetype : feed
date : 20-02-2022
---

When you pass an argument to a function in [[GO]], the function will behave differently depending on the type of the argument passed. Here we make a diffrerence between Value Types and [[GO Reference Types]]

With **Value Types**, go makes a copy of the value that you passed, and gives that copy to the function. This means that the function can't modify the original value of the variable you passed, as it's just getting a copy of the original value.

```go
package main

import "fmt"

type person struct {
	firstName string
	lastName string
}

func main() {
	p := person{
		firstName: "Jane",
		lastName: "Doe",
	}

	rename(p, "John")

	fmt.Println(p.firstName) // "Jane"
}

func rename(p person, newName string) {
	p.firstName = newName
}

```

You can work around this mechanism by passing a pointer instead of the value:

```go

package main

import "fmt"

type person struct {
	firstName string
	lastName string
}

func main() {
	p := person{
		firstName: "Jane",
		lastName: "Doe",
	}

	rename(&p, "John")

	fmt.Println(p.firstName) // "Jane"
}

func rename(p *person, newName string) {
	p.firstName = newName
}

```

Types that behave like this are:
- **int**
- **float**
- **string**
- **bool**
- **struct**


-----

Status: #💡 

