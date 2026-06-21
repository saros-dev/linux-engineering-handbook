# Navigation in Linux

> Navigation in Linux means moving through the filesystem efficiently using the shell. Since everything in Linux is represented as a file, mastering navigation is the foundation of working with any Linux system.

---

# Core Idea

Linux uses a **tree-like filesystem structure** starting from root:

```
/
├── home
├── etc
├── var
├── usr
└── bin
```

You move inside this tree using commands like `cd`, `ls`, and `pwd`.

---

# Key Concepts

## 1. Current Directory

The directory you are currently working in.

```bash
pwd
```

Example output:

```
/home/user/projects
```

---

## 2. Root Directory

The top of the filesystem:

```
/
```

Everything in Linux starts from here.

---

## 3. Home Directory

Each user has a personal directory:

```
/home/username
```

Shortcut:

```bash
cd ~
```

---

## 4. Absolute Path

A full path starting from root `/`.

Example:

```
/var/log/nginx/access.log
```

Usage:

```bash
cd /var/log
```

---

## 5. Relative Path

Path relative to current location.

Symbols:

```
.   → current directory
..  → parent directory
```

Example:

```bash
cd ..
cd ./docs
```

---

# Essential Commands

## 1. pwd (Print Working Directory)

Shows where you are.

```bash
pwd
```

---

## 2. ls (List Directory Contents)

List files and directories.

```bash
ls
```

Useful options:

```bash
ls -l     # detailed view
ls -a     # show hidden files
ls -lh    # human readable sizes
```

Example output:

```
-rw-r--r-- 1 user user  1.2K file.txt
drwxr-xr-x 2 user user  4.0K docs/
```

---

## 3. cd (Change Directory)

Move between directories.

```bash
cd /etc
cd ..
cd ~
cd -
```

Special case:

```bash
cd -
```

Returns to previous directory.

---

# Navigation Patterns

## Move into a directory

```bash
cd projects
```

## Go back one level

```bash
cd ..
```

## Jump to root

```bash
cd /
```

## Jump to home

```bash
cd ~
```

---

# Real-World Navigation Example

Imagine you're working on a server:

```bash
cd /var/log
ls
cd nginx
ls -l
cd ..
cd syslog
```

You are exploring logs step by step.

---

# Hidden Files

Files starting with `.` are hidden:

Example:

```
.bashrc
.gitignore
.config
```

Show them:

```bash
ls -a
```

---

# Directory Structure Insight

Linux follows **FHS (Filesystem Hierarchy Standard)**:

| Path | Purpose |
|------|--------|
| /etc | Configuration files |
| /var | Logs and variable data |
| /home | User data |
| /bin | Essential binaries |
| /usr | User programs |
| /tmp | Temporary files |

---

# Navigation Shortcuts

| Shortcut | Meaning |
|----------|--------|
| `~` | Home directory |
| `.` | Current directory |
| `..` | Parent directory |
| `-` | Previous directory |

Example:

```bash
cd -
```

---

# Common Mistakes

## 1. Confusing absolute vs relative paths

Wrong:

```bash
cd var/log
```

Correct:

```bash
cd /var/log
```

---

## 2. Deleting or modifying wrong directory

Always check location:

```bash
pwd
```

---

## 3. Losing track of directory

Recover with:

```bash
pwd
cd ~
```

---

# Useful Combinations

## Explore system logs

```bash
cd /var/log
ls -lh
```

## Go back and forth

```bash
cd /etc
cd -
cd -
```

## Search location before moving

```bash
pwd
ls
```

---

# Practical Exercise

Try this:

```bash
cd /
ls
cd etc
ls
cd ..
cd var/log
ls
```

This builds real navigation muscle memory.

---

# Key Takeaways

- Everything in Linux is inside a tree starting from `/`
- Navigation is about moving between directories efficiently
- `cd`, `ls`, and `pwd` are the core tools
- Absolute paths start from `/`
- Relative paths depend on current location
- `~`, `.`, `..`, `-` are essential shortcuts
```


## ➜ Next Chapter

👉 File Operations[./file-operations/file-operations.md]