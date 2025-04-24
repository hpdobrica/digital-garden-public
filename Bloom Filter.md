---
title : Bloom Filter
notetype : feed
date : 24-04-2025
---

Bloom filter is a fast, memory efficient probabilistic data structure that can quickly test whether an element is a member of a set.

It can return false positive results, but never false negative results - meaning that if it returns true, the element is probably in a set, but if it returns false, the element is definitely not in a set.

It is useful for things like [[LSM Tree]]s, where it can help us to quickly confirm whether a key exists in a database or not.

It works by:
- defining an array of bits `B`
- defining an array of hash functions `F` that each return a position of a bit in `B`
- adding a key
	- call each of the `F` hash functions with the key as input
	- in `B`, change bits at the positions returned by hash functions from 0 to 1
- checking a key
	- call each of the `F` hash functions with the key as input
	- check if returned bit indexes all have `1` as value

We can change the amount of false-positives we get by tweaking length of `B` and number of hash functions `F`.

Note that bloom filter as-is doesn't support deletions, but there is a variation which uses counters instead of bits that does.

## Example

Pseudocode example with simple hash functions:

```
bitArrayLen = 10
bitArray = new BitArray(bitArrayLen)
hashFunctions = [
	(key) => (sum of ASCII chars of key) % bitArrayLen
	(key) => (sum of ASCII chars * 2) % bitArrayLen
	(key) => (sum of ASCII chars * 3) % bitArrayLen
]

setKey(key) {
	hashFunctions.map(f => f(key)).forEach(bitIndex => {
		bitArray[bitIndex] = 1
	})
}

checkKey(key) {
	hashFunctions.map(f => f(key)).every(bitIndex => {
		return bitArray[bitIndex] == 1
	})
}

```

Using the above would look something like this:

```
setKey("apple")
// hashFunctions
	// 530 % 10 = 0
	// (530 * 2) % 10 = 1060 % 10 = 0
	// (530 * 3) % 10 = 1590 % 10 = 0
// bitArray (all 3 hash functions set bit at position 0 to 1)
	// [1, 0, 1, 0, 0, 0, 1, 0, 1, 0]

setKey("orange")
// hashFunctions
	// 636 % 10 = 6
	// (636 * 2) % 10 = 1272 % 10 = 2
	// (636 * 3) % 10 = 1908 % 10 = 8
// bitArray (this time we set bits 2, 6 and 8)
	// [1, 0, 1, 0, 0, 0, 1, 0, 1, 0]


checkKey("bananna") ❌
// hashFunctions return 9,8,7
// of these bits, only bit 8 has value 1, so bannana is deffinitely not in the set

checkKey("apple") ✅
// hash functions return 0,0,0, and bit 0 is set to 1 so this is POSSIBLY in a set, but not guaranteed as there are other keys which could end up having the hashes 0,0,0 as well
```

-----

Status: #📥

References:
- 
