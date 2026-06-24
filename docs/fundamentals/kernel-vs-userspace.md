# Kernel vs User Space

> Every Linux process runs in User Space, while the Linux kernel runs in Kernel Space.  
> This separation is one of the most fundamental concepts in Linux architecture and directly impacts security, stability, and performance.

---

# Overview

Linux divides execution into two isolated environments:

- User Space → where applications run
- Kernel Space → where the operating system core runs

This separation ensures that applications cannot directly access hardware or critical system memory.

---

# High-Level Architecture

```
+--------------------------------------------------+
|                  User Space                      |
|--------------------------------------------------|
| bash | nginx | python | docker | mysql | sshd    |
+--------------------------------------------------+
                      |
                      | System Calls
                      v
+--------------------------------------------------+
|                 Kernel Space                     |
|--------------------------------------------------|
| Process Scheduler                                |
| Memory Manager                                   |
| VFS (Virtual File System)                        |
| Network Stack                                    |
| Device Drivers                                   |
| Security Modules (SELinux, AppArmor)            |
+--------------------------------------------------+
                      |
                      v
+--------------------------------------------------+
|                   Hardware                       |
| CPU | RAM | Disk | NIC | GPU                     |
+--------------------------------------------------+
```

---

# User Space

User Space is where all applications execute.

Examples:

```
bash
zsh
nginx
python
node
docker
mysql
redis
```

## Characteristics

- Cannot access hardware directly
- Cannot access kernel memory
- Runs with limited privileges
- Each process is isolated

## What happens if a program crashes?

Only that process is affected:

```
python app.py → crash → only python dies
system remains stable
```

---

# Kernel Space

Kernel Space is the core of the operating system.

It has full access to:

- CPU instructions
- Physical memory
- Hardware devices
- Filesystems
- Network interfaces

## Kernel responsibilities

```
- Process scheduling
- Memory management
- Filesystem handling (VFS)
- Network stack (TCP/IP)
- Device drivers
- Security enforcement
```

---

# Why This Separation Exists

Without isolation:

```
Application
   ↓
Direct Hardware Access
   ↓
System-wide instability
```

A single bug could:

- Corrupt memory
- Crash the OS
- Leak sensitive data
- Break filesystem integrity

Linux solves this by enforcing strict separation.

---

# System Calls (The Bridge)

Applications cannot directly access kernel resources.

Instead they use system calls.

## Examples

```
open()
read()
write()
close()
fork()
execve()
socket()
mmap()
```

## Execution flow

```
Application
   ↓
glibc wrapper
   ↓
System Call
   ↓
Kernel
   ↓
Hardware / Resource
```

---

# Example: Reading a File

Command:

```bash
cat file.txt
```

Internal flow:

```
cat
 ↓
read()
 ↓
Kernel VFS
 ↓
Filesystem Driver (ext4/xfs)
 ↓
Disk
 ↓
Kernel buffer cache
 ↓
cat process
 ↓
Terminal output
```

Key point:
User space never touches the disk directly.

---

# Memory Model

Each process has its own virtual memory space:

```
+----------------------+
| Stack               |
+----------------------+
| Heap                |
+----------------------+
| Shared Libraries    |
+----------------------+
| Program Code        |
+----------------------+
```

The kernel maps virtual memory to physical memory using:

- Page tables
- MMU (Memory Management Unit)
- TLB (Translation Lookaside Buffer)

---

# Context Switching

When a process calls the kernel:

```
User Mode
   ↓
Kernel Mode
   ↓
Kernel Execution
   ↓
Return to User Mode
```

This transition is called **context switching**.

## Why it matters

It has overhead because CPU must:

- Save process state
- Switch privilege level
- Execute kernel code
- Restore state

Frequent context switches can reduce performance.

---

# Production Relevance

## Docker

Docker relies on kernel features:

- Namespaces (isolation)
- Cgroups (resource limits)
- Capabilities (privilege control)

---

## Nginx

Nginx uses kernel optimizations:

- epoll (efficient I/O multiplexing)
- sendfile (zero-copy file transfer)

---

## Databases

Databases rely heavily on:

- mmap()
- page cache
- async I/O

to reduce expensive system calls.

---

# Hands-On Commands

Observe system calls:

```bash
strace ls
```

Check kernel logs:

```bash
dmesg
```

View process memory:

```bash
cat /proc/self/maps
```

List file descriptors:

```bash
ls -l /proc/$$/fd
```

---

# Common Misconceptions

## Linux is an operating system

Incorrect.

```
Linux = Kernel
```

A full Linux system includes:

```
Kernel
+ GNU utilities
+ system libraries
+ package manager
```

---

## Applications can access hardware directly

False.

All hardware access goes through the kernel.

---

## Root user bypasses the kernel

No.

Even root operates through kernel mechanisms and restrictions.

---

# Interview Questions

## Basic

- What is User Space?
- What is Kernel Space?
- What is a system call?

## Intermediate

- Why do we need isolation?
- What happens during a system call?
- What is VFS?

## Advanced

- Why are system calls expensive?
- What is context switching?
- How does virtual memory work internally?
- How does Linux protect kernel memory?

---

# Key Takeaways

- User Space runs applications
- Kernel Space manages system resources
- System calls are the only bridge between them
- Isolation ensures stability and security
- Many modern systems (Docker, Kubernetes, Nginx, databases) depend heavily on kernel features



## ➜ Next Chapter

👉 [Linux Distributions](distributions.md)