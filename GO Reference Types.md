---
title : GO Reference Types
notetype : feed
date : 20-02-2022
---

When you pass an argument to a function in [[GO]], the function will behave differently depending on the type of the argument passed. Here we make a diffrerence between [[GO Value Types]] an Reference Types.

With **Reference Types**, go passes the reference to the value that you pass, allowing the called function to modify the original value of the argument.

```go

package main

import "fmt"

func main() {
	slice := []string{"Hello", "World"}

	modify(slice)

	fmt.Println(slice) // Hello Mom
}

func modify(s []string) {
	s[1] = "Mom"
}

```


Types that behave like this are:
- **slices**
- **maps**
- **channels**
- **pointers**
- **functions**


-----

Status: #💡 

