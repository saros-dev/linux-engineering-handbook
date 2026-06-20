# Linux Architecture

> Linux is a layered system designed around the Linux Kernel.  
> Everything in the system ultimately interacts with the kernel through system calls.

---

## 🧭 Overview

Linux follows a **layered architecture model**:

- Applications run in User Space
- Kernel runs in Kernel Space
- Communication happens via System Calls

This separation is the core of Linux design.

---

## 🧠 High-Level Architecture

```text id="arch1"
+--------------------------------------+
|          User Applications           |
|  (bash, nginx, python, docker)      |
+--------------------------------------+
|          System Libraries           |
|        (glibc, musl, etc.)          |
+--------------------------------------+
|          System Call Interface      |
|  (open, read, write, fork, exec)    |
+--------------------------------------+
|             Linux Kernel            |
|--------------------------------------|
| Process | Memory | FS | Network     |
+--------------------------------------+
|              Hardware               |
| CPU | RAM | Disk | NIC              |
+--------------------------------------+
```

---

## ⚙️ Why Architecture Matters

If you understand this architecture, you can:

- Debug production issues
- Understand performance bottlenecks
- Analyze memory leaks
- Understand container internals
- Understand networking issues
- Work with observability tools (strace, perf, eBPF)

---

## 🔵 User Space vs Kernel Space

```text id="space1"
USER SPACE                        KERNEL SPACE
+----------------------+        +----------------------+
| Applications         |        | Process Scheduler    |
| bash, nginx, python  |        | Memory Manager       |
| docker, system tools |        | Network Stack        |
+----------------------+        | File System (VFS)    |
                                 | Device Drivers       |
                                 +----------------------+
```

---

### 🟢 User Space

Runs:

- Applications
- Shells
- Services (nginx, sshd)

Characteristics:

- No direct hardware access
- Uses system calls
- Safe and isolated

---

### 🔴 Kernel Space

Runs:

- Core OS logic
- Drivers
- Scheduling system

Responsibilities:

- CPU scheduling
- Memory management
- I/O operations
- File systems
- Networking

---

## 🔗 System Call Mechanism

User applications cannot talk to hardware directly.

They must use **system calls**.

```text id="syscall1"
Application
    ↓
glibc wrapper
    ↓
System Call (open, read, write, fork)
    ↓
Kernel
    ↓
Hardware
```

---

### Example

```c
open("file.txt")
```

Becomes:

```text id="syscall2"
User Program → glibc → sys_open → Kernel → Filesystem → Disk
```

---

## 🧱 Kernel Subsystems

Linux kernel is modular.

### 1. Process Management

Handles:

- fork()
- exec()
- scheduling
- context switching

```text id="proc1"
Process → Scheduler → CPU Core
```

---

### 2. Memory Management

```text id="mem1"
Virtual Memory
      ↓
Paging System
      ↓
Physical RAM
      ↓
Swap (Disk)
```

Features:

- Isolation between processes
- Memory protection
- Page caching

---

### 3. Virtual File System (VFS)

Linux treats everything as a file.

```text id="vfs1"
ext4 / xfs / btrfs
        ↓
       VFS
        ↓
Unified file interface (/proc, /dev, /sys)
```

---

### 4. Networking Stack

```text id="net1"
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
Hardware (NIC)
```

---

### 5. Device Drivers

Bridge between:

- Kernel
- Hardware devices

Examples:

- Disk drivers
- GPU drivers
- Network drivers

---

## 🚀 How a Program Runs

Example:

```bash
./app
```

### Step-by-step flow:

```text id="run1"
Shell (bash)
    ↓ fork()
    ↓ exec()
Kernel loads binary
    ↓
Memory allocation
    ↓
Scheduler assigns CPU
    ↓
Process starts execution
```

---

## 📂 Real Example: File Read

```text id="file1"
Application → fopen()
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
lsblk           # storage devices
free -h         # memory usage
cat /proc/cpuinfo
cat /proc/meminfo
```

---

## 🚨 Real Production Scenarios

### High CPU Usage

Possible causes:

- Infinite loop in user space
- Kernel threads
- I/O wait

Tools:

```bash
top
htop
pidstat
```

---

### Memory Pressure

Possible causes:

- Memory leak
- Cache pressure
- Swap usage

Tools:

```bash
free -h
vmstat
dmesg | grep -i oom
```

---

### Disk / IO Issues

Symptoms:

- Slow response
- High iowait

Tools:

```bash
iostat
iotop
df -h
```

---

## 🎯 Interview Questions

### Basic
- What is Linux Kernel?
- What is user space?

### Intermediate
- What happens when you run a program?
- What is system call?

### Advanced
- What happens during context switching?
- How does Linux scheduling work?
- How does VFS work internally?

---

## 💡 Key Takeaways

- Linux is a layered architecture system
- Kernel is the core of everything
- User space never touches hardware directly
- System calls are the bridge
- Understanding flow is more important than memorization

---

## ➜ Next Chapter

👉 Kernel vs User Space (Deep Dive)