# Text Processing in Linux

> Linux becomes powerful when you treat everything as text and combine small tools to process, filter, transform, and analyze data streams.

---

# Overview

Almost everything in Linux is text-based:

- Logs (`/var/log`)
- Config files (`/etc`)
- Application output
- JSON / YAML files
- Network traces
- System diagnostics

Instead of using heavy tools, Linux provides small utilities that can be chained together using **pipes (`|`)**.

This philosophy is often summarized as:

> “Write programs that do one thing and do it well. Work together.”

---

# Core Concept: Streams

Linux processes data as streams:

```
Input → Processing → Output
```

There are 3 standard streams:

| Stream | Description |
|--------|-------------|
| stdin  | Input |
| stdout | Output |
| stderr | Errors |

Example:

```bash
echo "hello" | grep h
```

---

# The Power of Pipes

Pipe (`|`) connects commands:

```bash
command1 | command2 | command3
```

Example:

```bash
cat access.log | grep ERROR | wc -l
```

Flow:

```
log file → filter errors → count results
```

---

# Core Text Processing Tools

---

# 1. cat (Concatenate)

Displays file content.

```bash
cat file.txt
```

Use case:

- quick inspection
- piping into other commands

---

# 2. less (Pager)

Efficient file viewing.

```bash
less large.log
```

Features:

- search inside file (`/keyword`)
- scroll up/down
- handles huge files

---

# 3. head / tail

## head → first lines

```bash
head file.txt
```

## tail → last lines

```bash
tail file.txt
```

Live monitoring:

```bash
tail -f app.log
```

Used heavily in production debugging.

---

# 4. wc (Word Count)

Counts lines, words, bytes.

```bash
wc file.txt
```

Options:

```bash
wc -l   # lines
wc -w   # words
wc -c   # bytes
```

Example:

```bash
cat log.txt | wc -l
```

---

# 5. grep (Search Engine of Linux)

Search inside text.

```bash
grep "ERROR" app.log
```

Recursive search:

```bash
grep -r "ERROR" /var/log
```

Useful options:

```bash
-i   # ignore case
-n   # line numbers
-v   # invert match
```

Example:

```bash
grep -i "timeout" app.log
```

---

# 6. cut (Column Extractor)

Extract fields from structured text.

```bash
cut -d':' -f1 /etc/passwd
```

Example:

```
root:x:0:0:root:/root:/bin/bash
```

Output:

```
root
```

---

# 7. sort (Sorting Data)

```bash
sort file.txt
```

Reverse:

```bash
sort -r file.txt
```

Numeric sort:

```bash
sort -n numbers.txt
```

---

# 8. uniq (Remove Duplicates)

⚠ Works only on sorted data.

```bash
sort file.txt | uniq
```

Count duplicates:

```bash
sort file.txt | uniq -c
```

---

# 9. tr (Translate / Transform)

Character-level transformation.

Lowercase conversion:

```bash
echo "HELLO" | tr 'A-Z' 'a-z'
```

Replace characters:

```bash
echo "a,b,c" | tr ',' ' '
```

---

# 10. tee (Split Output)

Sends output to both file and terminal.

```bash
command | tee output.txt
```

Example:

```bash
ls | tee files.txt
```

---

# 11. xargs (Build Commands)

Converts input into arguments.

Example:

```bash
cat files.txt | xargs rm
```

Delete multiple files from list.

---

# Advanced Tools

---

# 12. sed (Stream Editor)

Used for text transformation.

Replace text:

```bash
sed 's/error/warning/g' file.txt
```

Delete lines:

```bash
sed '/DEBUG/d' file.txt
```

---

# 13. awk (Text Processing Language)

Column-based processing.

Print column:

```bash
awk '{print $1}' file.txt
```

Example (log analysis):

```bash
awk '{print $9}' access.log
```

Sum values:

```bash
awk '{sum+=$1} END {print sum}' numbers.txt
```

---

# Real-World Examples

---

# 1. Find error count in logs

```bash
grep ERROR app.log | wc -l
```

---

# 2. Top IP addresses in logs

```bash
cat access.log | awk '{print $1}' | sort | uniq -c | sort -nr
```

---

# 3. Find largest files

```bash
du -ah | sort -rh | head -10
```

---

# 4. Extract user list

```bash
cut -d':' -f1 /etc/passwd
```

---

# 5. Live monitoring errors

```bash
tail -f app.log | grep ERROR
```

---

# Mental Model

Think in pipelines:

```
Input → Filter → Transform → Sort → Output
```

Example:

```
logs → grep → awk → sort → uniq → report
```

---

# Why Text Processing Matters

Because in real systems:

- You don't debug with UI
- You debug with logs
- Logs are text
- Text is everything

Used in:

- DevOps pipelines
- Kubernetes debugging
- CI/CD logs
- Server monitoring
- Incident response

---

# Common Mistakes

## 1. Using grep without context

```bash
grep error file
```

Better:

```bash
grep -n error file
```

---

## 2. Forgetting sort before uniq

```bash
uniq file
```

Wrong results.

Correct:

```bash
sort file | uniq
```

---

## 3. Overusing cat

Bad:

```bash
cat file | grep error
```

Better:

```bash
grep error file
```

---

# Production Examples

---

## Nginx error analysis

```bash
grep 500 /var/log/nginx/access.log | wc -l
```

---

## System failures

```bash
journalctl -xe | grep failed
```

---

## High traffic IPs

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head
```

---

# Interview Questions

## Basic

- What is grep used for?
- Difference between head and tail?
- What does pipe do?

## Intermediate

- Why is sort required before uniq?
- Difference between cut and awk?

## Advanced

- How does pipeline execution work internally?
- What are stdin, stdout, stderr?
- Why is text processing critical in DevOps?

---

# Key Takeaways

- Linux processes everything as text
- Pipes connect small tools into powerful pipelines
- grep, awk, sed are core engineering tools
- Real-world debugging = log processing
- Mastering text processing = mastering Linux



## ➜ Next Chapter

👉 [Searching](../searching/searching.md)