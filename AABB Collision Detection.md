---
title : AABB Collision Detection
notetype : feed
date : 25-02-2022
---

Axis-Aligned Bounding Box is one of the simplest collision detection methods in 2d [[Game Development]], which only works on 2d rectangles that aren't rotated (their sides are parallel/perpendicular).

AABB works by checking if sides of rectangle A are outside of the opposite sides of rectangle B. For example, if top side of rectangle A is below bottom side of rectangle B, we know the two rectangles aren't colliding no matter what.

Given rectangles `A` and `B` with sides `top`, `bottom`, `left` and `right`, the formula we can use to check for collision would look something like this:

Collision is detected if all of these statements are true (just draw two rectangles and follow along):
- `A.left`  is to the left of `B.right`  
- `A.right` is to the right of `B.left` 
- `A.top` is above `B.bottom` 
- `A.bottom` is below `A.top`

We could represent the same idea in code like this:

```go

package main

type rectangle struct {
  x int
  y int
  width int
  height int
}

func main() {
  a := rectangle{x: 5, y: 5, width: 5, height: 5}
  b := rectangle{x: 3, y: 3, width: 5, height: 5}

  if (a.x < b.x + b.width) && 
     (a.x + a.width > b.x) && 
     (a.y < b.y + b.height) && 
     (a.y + a.height > b.y) {
	fmt.Println("Collision detected!")
  }
}


```

-----

Status: #🌲 

[[Status - Evergreen]]

[[Progress - Integrated]]




