---
title : Syscall
notetype : feed
date : 07-08-2022
---

In [[Linux]], whenever a user application wants to touch any of these:
- files
- any hardware or devices
- running processes
- networking stuff
- date/time
- writing to stdout
it can't do so on its own - it must ask Linux Kernel to do it instead.

**Syscall** is a way to ask Kernel to do something for you. The data is transfered between Kernel and the application using CPU registers, and the kernel is invoked using an interrupt (trap).

As many key functions are impossible without kernel, many of the programming language features rely on `syscall` under the hood.

For example in [[Golang]]:
- `fmt.Println` calls `Fprintln` with `os.Stdout` as an argument.
- `Fprintln` calls `write` function on `os.Stdout`
- `os.Stdout` is a `File` under the hood
- `File`'s `write` function finally invokes `syscall.Write`

As you can see, syscalls are often deeply abstracted, and their higher abstractions should always be used instead of syscalls directly (where available).

When invoked, `syscall`:
- saves the state of the CPU registers
- adds data about the syscall you are creating to the registers
- issues an interrupt (trap), letting the kernel know that there is something that needs to be done
- kernel then reads the info from the register, performs the operation, and writes the response back into the register
- `syscall` then resumes by reading the response from the register
- and finally restores the register to initial state (i assume as cleanup?)


We can see the syscalls that a process makes by using a tool called `strace`:
`strace -c echo "hello world"` will give us the count of all the syscalls made during execution of `echo "hello world"`.

`strace` itself actually accomplishes this by using Syscalls under the hood - by relying on `ptrace` syscall, it can see into the process and manipulate it. This is how breakpoint debuggers work.

It's possible to limit what syscalls a process can make for security reasons. For docker containers, we can do this with `seccomp`.

-----

Status: #💡 

References:
- [[Video - A Go Programmers guide to Syscalls]]
- [syscall man page](https://man7.org/linux/man-pages/man2/syscall.2.html)
