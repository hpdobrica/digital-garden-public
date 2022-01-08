---
title : Mode
notetype : unfeed
date : 06-01-2022
---

In statistics, Mode is the most common number in a data set.

```javascript

// not the actual way to do it, just pointing out the idea
const mode = (arr) => arr.reduce((acc, el) => {
	acc.counters[el] = acc.counters[el] ? acc.counters[el] + 1 : 1
	if(acc.max) {
		acc.max = acc.max < acc.counters[el] ? el : acc.max
	} else {
		acc.max = el
	}
}, {counters: {}, max: undefined}).max


const x = [1,1,2,3,4,5]

mode(x) // 1



```

-----

Status: #🌲 


