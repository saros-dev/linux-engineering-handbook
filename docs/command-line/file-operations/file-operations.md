# File Operations

> In Linux, files are the fundamental abstraction used to represent data, configuration, devices, processes, and communication endpoints. Understanding file operations is essential for system administration, automation, troubleshooting, and software development.

---

# Overview

Nearly every task in Linux involves interacting with files.

Examples:

- Editing configuration files
- Reading logs
- Managing application data
- Creating backups
- Deploying software
- Automating tasks

Linux follows a simple philosophy:

> Everything is a file.

This includes:

- Regular files
- Directories
- Symbolic links
- Block devices
- Character devices
- Sockets
- Pipes

Understanding how to create, copy, move, remove, inspect, and manipulate files is one of the most important Linux skills.

---

# File Types

Before learning file operations, it's important to understand the different file types.

## Regular Files

Store data.

Examples:

```text
notes.txt
config.yaml
app.py
```


Check file type:

```bash
file notes.txt
```

---

## Directories

Containers for files and other directories.

Example:

```text
/home/user/projects
```

Create directory:

```bash
mkdir projects
```

---

## Symbolic Links

References to another file or directory.

Example:

```text
current -> releases/v2
```

Create symbolic link:

```bash
ln -s releases/v2 current
```

---

## Device Files

Represent hardware devices.

Examples:

```text
/dev/sda
/dev/null
/dev/random
```

---

# Understanding Paths

All file operations depend on paths.

## Absolute Path

Starts from root.

```text
/etc/nginx/nginx.conf
```

---

## Relative Path

Starts from current directory.

```text
../config
./app.py
```

---

# Creating Files

## touch

Creates an empty file.

```bash
touch file.txt
```

Multiple files:

```bash
touch app.py config.yaml README.md
```

---

## Create File with Content

```bash
echo "Hello Linux" > file.txt
```

---

## Using Redirection

```bash
> file.txt
```

Creates file if it doesn't exist.

---

# Viewing Files

## cat

Display entire file.

```bash
cat file.txt
```

---

## less

View large files interactively.

```bash
less /var/log/syslog
```

Useful shortcuts:

```text
Space → next page
b     → previous page
q     → quit
```

---

## head

First lines.

```bash
head file.txt
```

Specific number:

```bash
head -n 20 file.txt
```

---

## tail

Last lines.

```bash
tail file.txt
```

Follow live updates:

```bash
tail -f application.log
```

Common for monitoring logs.

---

# Copying Files

## cp

Copy file:

```bash
cp source.txt destination.txt
```

---

## Copy Directory

```bash
cp -r project backup
```

---

## Preserve Metadata

```bash
cp -a source backup
```

Preserves:

- permissions
- ownership
- timestamps
- symbolic links

---

# Moving and Renaming

Linux uses the same command for both.

## Rename

```bash
mv old.txt new.txt
```

---

## Move

```bash
mv app.py src/
```

---

## Move Multiple Files

```bash
mv *.log logs/
```

---

# Deleting Files

## rm

Delete file:

```bash
rm file.txt
```

---

## Delete Multiple Files

```bash
rm *.tmp
```

---

## Delete Directory

```bash
rm -r project
```

---

## Force Delete

```bash
rm -rf project
```

Explanation:

```text
-r → recursive
-f → force
```

---

# Dangerous Commands

## Never Execute Blindly

```bash
rm -rf /
```

Attempts to remove the entire filesystem.

---

Always verify:

```bash
pwd
ls
```

before destructive operations.

---

# Creating Directories

## mkdir

```bash
mkdir project
```

---

## Create Nested Structure

```bash
mkdir -p projects/linux/docs
```

Without `-p`:

```bash
mkdir projects/linux/docs
```

fails if parent directories don't exist.

---

# Removing Directories

Empty directory:

```bash
rmdir temp
```

---

Non-empty directory:

```bash
rm -r temp
```

---

# File Metadata

Every file has metadata.

View details:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 user user 2456 Jan 10 app.py
```

Fields:

```text
Permissions
Links
Owner
Group
Size
Date
Filename
```

---

# Checking File Information

## stat

Detailed metadata:

```bash
stat file.txt
```

Shows:

- inode
- permissions
- timestamps
- ownership
- size

---

## file

Determine file type:

```bash
file nginx.conf
```

Example:

```text
ASCII text
```

---

# Symbolic Links

## Create

```bash
ln -s target.txt shortcut.txt
```

---

## Verify

```bash
ls -l
```

Output:

```text
shortcut.txt -> target.txt
```

---

## Remove Symlink

```bash
rm shortcut.txt
```

Target remains untouched.

---

# Wildcards (Globbing)

Linux shell supports pattern matching.

## All Files

```bash
*
```

Example:

```bash
ls *
```

---

## All Log Files

```bash
*.log
```

---

## Single Character

```bash
file?.txt
```

Matches:

```text
file1.txt
file2.txt
```

---

# Redirection and File Operations

## Overwrite Output

```bash
echo "hello" > file.txt
```

---

## Append Output

```bash
echo "new line" >> file.txt
```

---

## Redirect Errors

```bash
command 2> error.log
```

---

## Redirect Output and Errors

```bash
command > output.log 2>&1
```

---

# Real-World Examples

## Backup Configuration

```bash
cp -a /etc/nginx nginx-backup
```

---

## Archive Logs

```bash
mkdir logs-backup
cp *.log logs-backup/
```

---

## Rename Many Files

```bash
mv old.log old.log.bak
```

---

## Monitor Application Logs

```bash
tail -f application.log
```

---

# Common Mistakes

## Forgetting Recursive Copy

Wrong:

```bash
cp project backup
```

Error:

```text
omitting directory
```

Correct:

```bash
cp -r project backup
```

---

## Removing Wrong Directory

Always verify:

```bash
pwd
```

before:

```bash
rm -rf
```

---

## Overwriting Files Accidentally

Safer option:

```bash
cp -i source.txt destination.txt
```

Interactive confirmation.

---

# Production Relevance

File operations are involved in:

- Application deployments
- Log analysis
- Backup systems
- Configuration management
- CI/CD pipelines
- Container images
- Infrastructure automation

Most production incidents eventually require interacting with files.

---

# Hands-On Lab

Create environment:

```bash
mkdir linux-lab
cd linux-lab

touch app.py
touch config.yaml

mkdir logs

cp app.py backup.py

mv backup.py logs/

ls -R

rm logs/backup.py
```

---

# Interview Questions

## Basic

- Difference between cp and mv?
- Difference between file and directory?
- What does touch do?

## Intermediate

- What is a symbolic link?
- Difference between rm and rmdir?
- What does cp -a preserve?

## Advanced

- What is an inode?
- How do symbolic links work internally?
- What metadata does Linux store for files?

---

# Key Takeaways

- Everything in Linux revolves around files
- File operations are fundamental to system administration
- Always understand paths before modifying files
- Use recursive operations carefully
- Learn symbolic links and metadata inspection
- Mastering file operations significantly improves Linux productivity


## ➜ Next Chapter

👉 [Text Processing](../text-processing/text-processing.md)