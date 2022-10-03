---
title : Book - Concurrency in Go
notetype : unfeed
date : 25-09-2022
---


---

Source: [Concurrency in Go](https://www.oreilly.com/library/view/concurrency-in-go/9781491941294/)

Status: #🛈/📖/♻️ 

---

# 1 - introduction to concurrency

- concurrent - process that occurs simultaneously with one or more processes
- Moore's law - number of components on an integrated circuit will double every two years (held true until 2012)
- people started looking for other ways to incr ase computational power - mainly by building multi core processors
- amadahl's law then became a problem - performance gains from parallel computing are bounded by how much the program must be written in sequential manner
- in some processes you have bottlenecks which reduce the usefulness of high number of cores ( UI application bounded by user input), while some others are embarrassingly parallel (yep, actual term), meaning that you can divide it to many cores, and just care about combining the results
- embarrassingly parallel problems should have solutions that scale horizontally
- in order to do that effectively, we have to figure out how to utilize cloud computing, as well as how to structure our code concurrently

## why is concurrency hard?

- race conditions
	- occurs when successful execution requires a specific order of operation, but the software is not written in a way that guarantees this order
	- one of most common race conditions is a data race, where one concurrent operations tries to read some variable, while another writes to it
	- problem arises because of sequential thinking - operation is defined first, so it will happen first
	- it helps to think of what would happen if concurrent code got to execute an hour in the future
	- adding sleeps seems to resolve the issue, but it only makes the issue less likely to happen - the program will never be logically correct
	- race conditions can sometimes become apparent a long time after the code has went to production, making them difficult to track
- atomicity
	- means that the thing is not divisible in it's context of operation
	- operation scope is the first thing that should be defined when thinking about atomicity, as an operation can be atomic in one context (eg your process), but not in another (eg your os)
	- wow glider bot avoided detection by anti cheat system by utilizing system interrupts - while anti cheat scan was atomic within the context of the process, in the context of the os it was not
	- i++ seems atomic, but is consisted of 3 atomic operations: retrieving the value, incrementing it and storing it
		- in some contexts like non-concurrent program, these 3 operations make up a bigger atomic operation
		- having a goroutine that doesn't expose i to other goroutines also makes the operation atomic
		- in other cases, it may not be atomic
	- since many statements aren't atomic, we can't expect functions and programs to be - so we need a way to force atomicity to make sure our programs are logically correct
- memory access synchronization
	- critical section is a part of a program that requires exclusive access to a shared resource
	- we can give exclusive memory access to a critical section by locking the memory before using it, and unlocking it after we are done
	- adding memory locking to an example where a goroutine increments a value while main process reads it, solves the data race (they won't access the data at the same time), but doesn't solve race condition (nothing guarantees who will acquire the lock first)
	- making a convention to lock memory in critical sections, doesn't make it impossible for someone to forget the lock
	- in addition to not being enough to make the program logically correct, locking memory can also slow the program down
	- since every time critical section happens stops the part of our program, we must ask:
		- are they entered and exited repeatedly?
		- what size should my critical sections be?
- deadlocks, lovelocks and starvation
	- are issues that arise when we implement other solutions to achieve logical correctness, and that concern with your program having something to do at all times
	- deadlocks
		- deadlocked program is a program in which all concurrent processes are stopped waiting for one another
		- run two goroutines locking two values one at a time, goroutine 1 locks A and then B, while goroutine 2 locks B and then A - this will lead to a being locked by routine 1, which is now waiting for lock of B, which it will never acquire since B is locked by routine 2, which is waiting to acquire a lock on A
		- Coffman conditions are preconditions that must happen for a deadlock to arise:
			- mutual exclusion - a concurrent process holds exclusive rights to a resource at any one time
			- wait for condition - a concurrent process must hold a resource and simultaneously wait for additional resource
			- no preemption - a resource held by a concurrent process can only be released by that process
			- circular wait - a concurrent process P1 must wait on chain of concurrent processes P2, which are in turn waiting on P1
		- preventing any one of these conditions stops a deadlock, which might sound simple but it's really hard to reason about
	- livelock 
		- livelocks happen when program is actively running concurrent operations, but there operations do nothing to move the state of the program forward
		- like trying to pass a person on the street where both of you try to move away in the same direction - just forever
		- common reason for livelocks to happen is when multiple processes try to resolve a deadlock without coordination
		- livelocks are a subset of a larger set of problems called starvation 
	- starvation
		- starvation is any situation when a concurrent process can't get all the resources it needs to perform work
		- livelocks are a special case where two processes are equally starved of a shared lock
		- standard starvation usually occurs when we have a greedy process that stops others from accomplishing their tasks, either effectively or at all
		- imagine two workers, one locking a resource and performing all it's work, and the other just locking for each iteration of the work it needs, releasing the lock between iterations - first is greedily using locks and will end up getting much more work done at the expense of a polite worker
		- a way to detect starvation is measuring the completed work and comparing it to expected work
		- looking only critical sections prevent starvation, but it might have performance implications - by widening our look beneath critical section, we increase performance but also starvation
		- a good way to find balance is to always start from locking just critical sections and then widen the lock if performance is a problem
		- starvation can cause inefficiency but also incorrectness in case where one process is so greedy that other processes cannot perform their work at all
		- starvation can also come from outside of the process, for example CPU, memory, etc... any resource that must be shared is a candidate for starvation
	- determining concurrency safety
		- having a concurrent function can make it unclear whether you are responsible for institiating multiple concurrent invocations of this function and who is responsible for maintaining the lock over the resources
		- having clear comments on these topics can help immensely
		- within your concurrent functions comments always cover these three topics
			- who is responsible for the concurrency
			- how is the problem space mapped onto concurrency primitives
			- who is responsible for this? synchronization
		- in addition to comments having clearer function signature can make concurrency topics clearer
		- `func CalculatePi(begin, end int64, pi *Pi)`
			- is it concurrent?
			- am i supposed to invoke it concurrently?
			- should i lock access to *Pi
		- `func CalculatePi(begin, end int64) []uint`
			- is it concurrent?
		- `func CalculatePi(begin, end int64) <- chan uint`
			- all clear, but might have performance implications
- how go helps 
	- very fast garbage collection
	- Goroutines allow you not to deal with starting , managing threads and mapping logic evenly across available threads
	- Go primitives like channels give you a easy concurrent safe way to communicate between concurrent processes
	- 

# 2 - modeling your code: communicating sequential processes

- concurrency is a property of the code while parallelism is a property of a running system
- we can write code to be concurrent and it might run parallelly on some machines while it wouldn't on others. (machine with one core versus multiple cores)
- when writing our code, we should be ignorant on how many cores it's running
- we have many layers of abstraction allowing us not to think about this - safest example being that processes running on two different machines can't affect each other and are running completely in parallel. the deeper you go with the abstractions, the more work is required to achieve safe parallelism
- base abstraction developers generally work with to achieve parallelism is os thread
- go makes this easier by providing goroutines and channels based on paper "communicating sequential processes"
- what is csp?
	- "mock language" to demonstrate a way to communicate between processes
	- later csp ideas were reformed into "process calculus", a way to mathematically model concurrent systems
	- inputs and outputs need to be considered language primitives
	- shared memory is difficult but not always bad (tools in go in `sync` package)
- goroutines allow us to think less of parallelism and model our code for concurrency - focus more on the problem of the domain, less on the problem of os threads
- go is designed with concurrency in mind so you don't have to rely on a library to provide this for you - less abstractions, less bugs
- parallelism is handled outside our code, so our code benefits from future advancements without us having to touch it
- go docs generally say that memory sync should be used by low level packages, and that csp constructs should be preferred way to handle concurrent code
- on the other hand, a lot of memory sync constructs are in use, there are people thinking that channels are overused, so it is good to have understanding of how both work
- go wiki says to use whichever is the most expressive or most simple of the two
- what should I use (2-1 flow chart)
	- if it's performance critical, use primitives
		- this doesn't mean "this code should be performant" but "we are hitting a bottleneck here and primitives must be a bit faster since channels use them under the hood, we should consider refactoring"
	- if trying to transfer ownership of data, use channels
		- e.g. part of code produces some data and wants to share that result with another piece of code
	- if trying to guard internal state of a struct, use primitives
		- having a struct with internal lock would allow it to be atomic in the scope of that struct. in this scenario, exposing lock variable would be a red flag
	- if trying to coordinate multiple pieces of logic, use channels
		- having lock objects scattered throughout your application sounds like introduction to disaster, channels are much more composable
- os thread patterns should generally be discarded when working with go
- you are more likely to hit a problem where you need to restructure your program than a problem of hitting the upper limit of goroutines your hardware can support
- aim for simplicity, use channels when possible, treat goroutines like a free resource

## 3 - Go's concurrency building blocks

- goroutine is a function that is running concurrently alongside other code, and are created by placing go keyword before the function invocation
- they are not os threads, but a higher level of abstraction known as coroutine
- coroutines are concurrent subroutines (functions, closures, methods in go) that are nonpreemtive (cannot be interrupted). instead, coroutines have multiple points that allow suspension or reentry
- goroutines are deeply integrated in go's runtime and instead of defining their own suspension and entry points, go runtime observes them, suspending them when they block and resuming when they become unblocked - in other words, they are preemtible only when blocked
- in order for them to run concurrently, something must host several goroutines simultaneously to provide the concurrency (and optionally parallelism) 
	- go uses `M:N Scheduler` for this - mapping of M green threads to N os threads
	- goroutines are then scheduled on the green threads
	- if there are more goroutines than green threads available, scheduler distributes them across available threads and ensures that if these goroutines become blocked, others can run
- go uses `fork-join` concurrency model
	- fork - at any time program can split a child branch of execution to be run concurrently with its parent
	- join - at some point in the future (known as a join point), these concurrent branches will join back together ( #TODO testing image stuff)
![[markup_File_20221003-090633.jpg.png]]

```go
func main(){
  sayHello := func(){
    fmt.Println("hello")
  }
  go sayHello()
}
```

- in the example above, nothing guarantees that the line will be printed. this is because the main routine might exit before the goroutine has started executing.go sayHello only schedules the go routine - there is no join point
- sleep would be a way to make the line print, but that's not a valid option - we need a join point to guarantee applications logical correctness
- one way to create a join point is to synchronize main goroutine with sayHello goroutine using sync.WaitGroup

```go

func main(){
  var wg sync.WaitGroup
  sayHello := func() {
    defer wg.Done()
    fmt.Println("hello")
  }

  wg.Add(1)

  go sayHello() 
  wg.Wait() // join point
}

```
- goroutine closures run in the same address space they are created in, so they can modify the variables that are provided to them by their lexical scope
- having a for range loop which creates a goroutine for each iteration will likely end up with the last value of the iterating slice - similar like in javascript
- since the goroutines might not get to execute before the for range is done, (instead of iterating variable disappearing from memory because it went out of scope) go runtime will notice that the iterating variable is still held by closure and will move this piece of memory to the heap, so that goroutines can still access it
- the problem of the last value being printed all times is also resolved like in js - by passing the value as a parameter into the closure instead of relying on the lexical scope
- since all of the goroutines will have access to the same address space, we must take care of managing memory access between them, either via primitives or csp constructs
- goroutines are pretty lightweight
- they won't be garbage collected if they block
- context switching in os threads is pretty expensive - using software scheduler makes this much cheaper in go
- the sync package
	- 
