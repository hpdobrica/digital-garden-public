---
title : Linear Interpolation
notetype : feed
date : 20-11-2021
---

Linear interpolation (commonly refered to as **lerp**) is a useful function in the fields of [[Public/Game Development]] and [[Creative Coding]]. It's used to get a number on a specific point between two numbers. 

The parameters are the `start` and `end` of the desired range, as well as `t` which represents a number between 0 and 1. Setting `t=0` would give you the start value you provided, setting `t=1` would give the end value you provided, while setting it `t=0.5` would give the value exactly in between the `start` and `end`.

```go

func Lerp(start, end, t float64) float64 {
	return start*(1-t) + end*t
}

```

Let's look at some examples:

```go

Lerp(0, 100, 0) // returns the start value, 0
Lerp(0, 100, 1) // returns the end value, 100
Lerp(0, 100, 0.5) // returns the value exactly in between, 50

Lerp(-5, 5, 0.5) // returns 0
Lerp(100, 10, 0) // returns 100, the interpolation can go in reverse too!

```


-----

Status: #🌲 


