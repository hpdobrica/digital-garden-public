---
title : Video - A Go Programmers guide to Syscalls
notetype : feed
date : 07-08-2022
---

Source: [GopherCon 2017: Liz Rice - A Go Programmer's Guide to Syscalls](https://www.youtube.com/watch?v=01w7viEZzXQ)

Status: #🛈/📹/✅ 

POC: https://github.com/hpdobrica/go-playground/tree/main/strace

------

- [[Syscalls]] is a way for a program running in userspace to request sevices from the kernel of [[Linux]] OS
- program can't touch these without kernel/syscalls:
	- files
	- devices
	- processes
	- communications/networking
	- date/time
	- even writing to stdout
- `strace` is a tool allowing us to see syscalls made by a process
	- `strace -c ./myapp` gives us a summary of all syscalls made
- `fmt.Println` in go uses a write syscall under the hood:
	- `Println` calls `Fprintln` and passes it `os.Stdout`
	- `Fprintln` calls `write` on `os.Stdout`
	- `Stdout` is created with `NewFile`  (at `/dev/stdout`) which creates a `File`
	- inside of `File` there is finally a call to `syscall.Write`
- [[Golang]] `syscall` package is a low level package that makes it easier to create syscalls
	- implementation varies by os/hardware
	- shouldn't be used if there is a high-level alternative
	- its pretty much a wrapper around the OS, so for details on how to use it and what each syscall does, you'd have to look up the manual for your platform
	- In the end they all call `Syscall()` with different parameters - in this example `Syscall(SYS_WRITE)`
	- there is about 300 of them on linux: https://pkg.go.dev/syscall#pkg-constants
- what does `Syscall` do?
	- saves register state before making changes (?)
	- sets up a register with the details about syscall you are making
	- issues a trap (an interrupt saying - ok kernel, i need you to do something for me)
	- kernel reads info from the register, does its job and writes the response back to the register
	- application reads the response from the register
	- and finally restores register to the initial state from step 1 (?)
- implementing syscall layer allows you to emulate linux (e.g. bash on windows)
- `ptrace` is a syscall that allows `strace`-like tools to see into the processes and manipulate them
	- allows us to manipulate registers and memory of another process
	- it's primarily used for implementing breakpoint debugging and syscall tracing
	- in go there is a lot of ptrace subcommands that are all helpers that wrap around `SYS_PTRACE`
- building our own `strace`
	- when starting a process with ptrace, it will end up in a breakpoint-like state
	- once your process exits, there is nothing holding that breakpoint so the child process will continue working
	- while breakpointed we can issue syscall to read the registers
	- name of the currently running syscall can be fetched from `Orig_rax` register
	- `execve` is name of syscall that happens when we want to create a new process
	- `PTRACE_SYSCALL` will restart the child process and make it stop on the next syscall, allowing us to move forward
	- `syscall.wait4` allows us to wait for the next interrupt
	- we can loop through the whole program and see all syscalls by:
		- `syscall.PtraceGetRegs` + extract the name of the current syscall
		- `syscall.PtraceSyscall` to let it run to the (exit or enter of) next syscall
		- `syscall.Wait4` to make it wait for the interrupt of the next syscall to happen
	- because `PtraceSyscall` triggers on enters and exits, we will have to keep track of the state ourselves
- syscalls and security
	- for microservice architecture, it might make sense to approach syscalls with the principle of least privilege, and limit syscalls a process can make
	- `seccomp` can be used to limit syscalls of a process:
		- e.g. `docker run --security-opt seccomp=/path/sc_profile.json hello-world`
		- we can similarily implement a filter that will enable us to dissalow a syscall in a process