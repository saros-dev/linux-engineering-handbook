# Linux Architecture

> Linux is a layered system built around the Linux Kernel. Understanding its architecture is essential for debugging, performance tuning, and system design.

---

## 🧠 High-Level Overview

Linux follows a layered architecture:

```text
+-----------------------------------+
|        User Applications          |
| (bash, nginx, python, docker)     |
+-----------------------------------+
|       System Libraries            |
|        (glibc, etc.)              |
+-----------------------------------+
|         System Calls              |
|   (open, read, write, fork)      |
+-----------------------------------+
|           Linux Kernel            |
|-----------------------------------|
| Process | Memory | FS | Network   |
+-----------------------------------+
|            Hardware               |
| CPU | RAM | Disk | NIC            |
+-----------------------------------+
```

---

## ⚡ Why This Matters

This architecture helps you understand:

- Why processes crash
- Why memory leaks happen
- How containers work
- Why CPU spikes occur
- How networking actually functions
- How system calls bridge apps and kernel

---

## 🔵 User Space vs Kernel Space

```text
USER SPACE                         KERNEL SPACE
+------------------+              +----------------------+
| Applications     |              | Process Scheduler    |
| bash, nginx      |              | Memory Manager       |
| python, docker   |              | Network Stack        |
+------------------+              | File System (VFS)    |
                                  | Device Drivers       |
                                  +----------------------+
```

### Key Difference

| User Space | Kernel Space |
|------------|-------------|
| Limited access | Full hardware access |
| Safe | Critical |
| Uses system calls | Direct hardware control |

---

## 🔗 System Call Flow

When a program wants to access hardware:

```text
Application
    ↓
glibc wrapper
    ↓
System Call (open, read, write)
    ↓
Linux Kernel
    ↓
Driver / Hardware
```

### Example

```c
open("file.txt")
```

Becomes:

```text
User App → glibc → sys_open → Kernel → Disk
```

---

## ⚙️ Linux Kernel Internals

Inside the kernel:

```text
+-----------------------------+
| Process Scheduler          |
| Memory Manager             |
| Virtual File System (VFS)  |
| Networking Stack           |
| Device Drivers            |
+-----------------------------+
```

---

### 🧵 Process Management

- fork()
- exec()
- wait()
- kill()

Kernel is responsible for:

- creating processes
- switching context
- scheduling CPU time

---

### 🧠 Memory Management

```text
Virtual Memory
     ↓
Paging System
     ↓
Physical RAM
     ↓
Swap (Disk)
```

Kernel ensures:

- isolation between processes
- memory safety
- paging/swapping

---

### 📁 File System (VFS)

Linux treats everything as a file:

```text
Disk → ext4 / xfs / btrfs
             ↓
           VFS
             ↓
   unified file interface
```

Examples:

- /dev/sda → disk
- /proc → process info
- /sys → kernel info

---

### 🌐 Networking Stack

```text
Application
    ↓
Socket API
    ↓
TCP / UDP
    ↓
IP Layer
    ↓
Network Driver
    ↓
NIC (Network Card)
```

---

## 🚀 How a Program Runs

Example:

```bash
./app
```

Flow:

```text
Shell (bash)
   ↓ fork()
   ↓ exec()
Kernel loads binary
   ↓
Memory allocated
   ↓
Scheduler assigns CPU
   ↓
Process runs
```

---

## 📂 Real Example: Reading a File

```text
App → fopen()
    ↓
glibc
    ↓
open() syscall
    ↓
Kernel VFS
    ↓
Filesystem driver
    ↓
Disk
```

---

## 🧪 Useful Commands

```bash
uname -a        # kernel info
lscpu           # CPU info
lsblk           # disks
free -h         # memory
cat /proc/cpuinfo
cat /proc/meminfo
```

---

## 🚨 Real Production Issues

### High CPU

```text
Process stuck → CPU spike → scheduler pressure
```

Tools:

```bash
top
htop
pidstat
```

---

### Memory Leak

```text
App allocates memory → never frees → swap usage → OOM
```

Tools:

```bash
free -h
vmstat
dmesg | grep -i oom
```

---

## 🎯 Interview Questions

### Basic
- What is Linux Kernel?
- What is user space?

### Intermediate
- What happens when you run a program?
- What is a system call?

### Advanced
- How does context switching work?
- What happens inside fork()?

---

## 💡 Key Takeaways

- Linux is layered, not monolithic in usage
- Kernel is the core of everything
- System calls are the bridge between worlds
- Understanding flow > memorizing commands

---

## ➜ Next Chapter

👉 Kernel vs User Space (Deep Dive)