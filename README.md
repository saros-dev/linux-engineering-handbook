![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active-brightgreen)
![Open Source](https://img.shields.io/badge/open--source-yes-blue)



# Linux Engineering Handbook

> A structured, open-source Linux handbook for DevOps Engineers, SREs, Platform Engineers, System Administrators, and backend engineers who want deep understanding of Linux systems.

---

## About This Project

This repository is a **Linux-focused engineering knowledge base** covering everything from basic command-line usage to deep Linux internals.

It is NOT a cheat sheet.

It is NOT a DevOps tool collection.

It is a structured learning system for understanding how Linux actually works.

---

## What You Will Learn

- How Linux is structured internally
- How processes, memory, and CPU scheduling work
- How networking is implemented in Linux
- How filesystems and storage work
- How permissions and security are enforced
- How system services (systemd) operate
- How containers use Linux internals
- How to debug real production issues
- How to think like a Linux engineer

---

## Learning Path

```text
Fundamentals
    ↓
Command Line
    ↓
Filesystem
    ↓
Users & Groups
    ↓
Permissions
    ↓
Processes
    ↓
Memory Management
    ↓
CPU Scheduling
    ↓
Systemd
    ↓
Networking
    ↓
Storage
    ↓
Security
    ↓
Shell Scripting
    ↓
Logging & Observability
    ↓
Performance Tuning
    ↓
Troubleshooting
    ↓
Linux Internals
    ↓
Containers (Linux-level)
```

---

## Table of Contents

### 1. Fundamentals
- [Linux History](docs/fundamentals/linux-history.md)
- [Unix vs Linux](docs/fundamentals/unix-vs-linux.md)
- [Linux Architecture](docs/fundamentals/linux-architecture.md)
- [Kernel vs User Space](docs/fundamentals/kernel-vs-userspace.md)
- [Linux Distributions](docs/fundamentals/distributions.md)

---

### 2. Command Line
- [Navigation](docs/commands/navigation.md)
- [File Operations](docs/commands/file-operations.md)
- [Text Processing](docs/commands/text-processing.md)
- [Searching](docs/commands/searching.md)

---

### 3. Filesystem
- [Filesystem Hierarchy](docs/filesystem/filesystem-hierarchy.md)
- [Inodes](docs/filesystem/inode.md)
- [File Types](docs/filesystem/file-types.md)
- [Mount Points](docs/filesystem/mounts.md)

---

### 4. Users & Groups
- [Users](docs/users-groups/users.md)
- [Groups](docs/users-groups/groups.md)
- [Sudo](docs/users-groups/sudo.md)

---

### 5. Permissions
- [chmod](docs/permissions/chmod.md)
- [chown](docs/permissions/chown.md)
- [ACL](docs/permissions/acl.md)

---

### 6. Processes
- [Process Lifecycle](docs/processes/process-lifecycle.md)
- [Signals](docs/processes/signals.md)
- [Process Monitoring](docs/processes/process-monitoring.md)

---

### 7. Memory Management
- [Virtual Memory](docs/memory/virtual-memory.md)
- [Swap](docs/memory/swap.md)
- [OOM Killer](docs/memory/oom-killer.md)

---

### 8. CPU Scheduling
- [Process Scheduling](docs/cpu/scheduling.md)
- [Nice & Priority](docs/cpu/nice-priority.md)

---

### 9. Systemd
- [Systemd Basics](docs/systemd/basics.md)
- [Services](docs/systemd/services.md)
- [Journal Logs](docs/systemd/journal.md)

---

### 10. Networking
- [TCP/IP Model](docs/networking/tcp-ip.md)
- [DNS](docs/networking/dns.md)
- [Routing](docs/networking/routing.md)
- [Network Troubleshooting](docs/networking/troubleshooting.md)

---

### 11. Storage
- [Partitions](docs/storage/partitions.md)
- [LVM](docs/storage/lvm.md)
- [RAID](docs/storage/raid.md)

---

### 12. Security
- [Linux Permissions Model](docs/security/permissions.md)
- [SELinux](docs/security/selinux.md)
- [AppArmor](docs/security/apparmor.md)
- [Firewall Basics](docs/security/firewall.md)

---

### 13. Shell Scripting
- [Bash Basics](docs/shell/basics.md)
- [Variables & Conditions](docs/shell/variables.md)
- [Loops](docs/shell/loops.md)
- [Automation Scripts](docs/shell/automation.md)

---

### 14. Logging & Observability
- [Linux Logs](docs/logging/logs.md)
- [Journalctl](docs/logging/journalctl.md)
- [Monitoring Tools](docs/logging/monitoring.md)

---

### 15. Performance Tuning
- [CPU Profiling](docs/performance/cpu.md)
- [Memory Profiling](docs/performance/memory.md)
- [Disk I/O](docs/performance/io.md)

---

### 16. Troubleshooting Playbooks
- [High CPU Usage](playbooks/high-cpu.md)
- [High Memory Usage](playbooks/high-memory.md)
- [Disk Full](playbooks/disk-full.md)
- [Network Issues](playbooks/network-issues.md)
- [DNS Failure](playbooks/dns-failure.md)

---

### 17. Linux Internals
- [System Calls](docs/internals/system-calls.md)
- [ELF Binaries](docs/internals/elf.md)
- [Process Creation (fork/exec)](docs/internals/process.md)
- [Memory Layout](docs/internals/memory-layout.md)
- [Cgroups](docs/internals/cgroups.md)
- [Namespaces](docs/internals/namespaces.md)

---

### 18. Containers (Linux Level)
- [What are Containers](docs/containers/intro.md)
- [Namespaces](docs/containers/namespaces.md)
- [Cgroups](docs/containers/cgroups.md)
- [OverlayFS](docs/containers/overlayfs.md)
- [How Docker Uses Linux](docs/containers/docker-internals.md)

---

### 19. Labs
Hands-on practice environments:
- Users & Permissions Lab
- Networking Lab
- Systemd Lab
- Filesystem Lab
- Troubleshooting Lab

---

### 20. Playbooks
Real-world production scenarios:
- Server is Slow
- Disk is Full
- High CPU Investigation
- Memory Leak Debugging
- Network Latency Issues

---

## Contributing

Contributions are welcome.

Please open an issue or submit a pull request.

---

## License

This project is licensed under the MIT License.