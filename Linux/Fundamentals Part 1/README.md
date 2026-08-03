# Linux Fundamentals Part 1

## Overview

In this room, I learned the fundamentals of the Linux operating system, including terminal usage, filesystem navigation, file searching, and shell operators. These concepts are essential for system administration, penetration testing, and cybersecurity.

---

# 1. Introduction to the Linux Terminal

## What is the Linux Terminal?

The Linux terminal is a **command-line interface (CLI)** that allows users to interact with the operating system by typing commands instead of using a graphical user interface (GUI).

Many Linux servers do not include a GUI because it reduces resource usage and improves performance. As a result, learning to use the terminal is one of the most important Linux skills.

> **Note:** Ubuntu Server can operate without a graphical desktop environment, making it lightweight and widely used for servers.

---

## Commands Learned

### `echo`

The `echo` command displays text in the terminal.

### Syntax

```bash
echo Hello
echo "Hello Friend!"
```

### Example Output

```text
Hello
Hello Friend!
```

### Notes

- Double quotation marks are **optional** when printing a single word.
- Use quotation marks when the text contains spaces.

Example:

```bash
echo Hello
```

```bash
echo "Hello Friend!"
```

---

### `whoami`

The `whoami` command displays the username of the currently logged-in user.

### Syntax

```bash
whoami
```

### Example Output

```text
tryhackme
```

### Practical Use

This command is useful for confirming which user account is currently running commands, especially after switching users or connecting to a remote Linux machine.

---

## Key Concepts

- Linux servers are often managed entirely through the terminal.
- The terminal provides a fast and efficient way to interact with the operating system.
- Learning basic commands is the foundation of Linux and cybersecurity.

---

## Summary

In this section, I learned how to:

- Use the Linux terminal.
- Display text using the `echo` command.

---

# 2. Filesystem Navigation

## Overview

Navigating the Linux filesystem is one of the most fundamental skills for working with Linux systems. Since many Linux environments do not include a graphical interface (GUI), users must rely on terminal commands to browse directories, locate files, and read their contents.

In this section, I learned how to move through the filesystem and interact with files using essential Linux commands.

---

## Commands Learned

| Command | Description |
|---------|-------------|
| `ls` | Lists files and directories. |
| `cd` | Changes the current working directory. |
| `cat` | Displays the contents of a file. |
| `pwd` | Prints the current working directory. |

---

## `ls` — List Directory Contents

The `ls` command displays the files and directories located in the current directory.

### Syntax

```bash
ls
```

### Example

```bash
ls
```

**Output**

```text
Important Files
My Documents
Notes
Pictures
```

### Tip

You can list the contents of another directory without entering it.

```bash
ls Pictures
```

---

## `cd` — Change Directory

The `cd` command changes your current working directory.

### Syntax

```bash
cd Pictures
```

### Example

```bash
cd Pictures
ls
```

**Output**

```text
dog_picture1.jpg
dog_picture2.jpg
dog_picture3.jpg
dog_picture4.jpg
```

### Tip

You can navigate directly to any directory using its absolute path.

```bash
cd /home/ubuntu/Documents
```

---

## `cat` — Display File Contents

The `cat` command displays the contents of a file directly in the terminal.

### Syntax

```bash
cat todo.txt
```

### Example

```bash
ls
```

**Output**

```text
todo.txt
```

```bash
cat todo.txt
```

**Output**

```text
Here's something important for me to do later!
```

### Tip

You can read a file without changing directories by providing its full path.

```bash
cat /home/ubuntu/Documents/todo.txt
```

---

## `pwd` — Print Working Directory

The `pwd` command displays the absolute path of your current working directory.

### Syntax

```bash
pwd
```

### Example

```bash
pwd
```

**Output**

```text
/home/ubuntu/Documents
```

Knowing your current location is important when navigating large Linux systems.

---

## Cybersecurity Relevance

Filesystem navigation is an essential skill for cybersecurity professionals.

These commands are commonly used to:

- Navigate target systems during penetration testing.
- Locate configuration files.
- Find log files for forensic analysis.
- Read passwords, flags, or configuration files during Capture The Flag (CTF) challenges.
- Inspect directories after gaining shell access to a Linux machine.

---

## Key Takeaways

- `ls` lists files and directories.
- `cd` changes the current directory.
- `cat` displays the contents of a file.
- `pwd` prints the absolute path of the current directory.
- Understanding filesystem navigation is fundamental for Linux administration and cybersecurity.

---

# 3. Finding Files and Searching

## Overview

As Linux systems grow in size, manually searching through directories becomes inefficient. Linux provides powerful command-line tools that allow users to quickly locate files and search within their contents.

In this section, I learned how to use the `find`, `grep`, and `wc` commands to efficiently search files and analyze text.

---

## Commands Learned

| Command | Description |
|---------|-------------|
| `find` | Searches for files and directories. |
| `grep` | Searches for specific text within files. |
| `grep -R` | Recursively searches through directories and subdirectories. |
| `wc -l` | Counts the number of lines in a file. |

---

## `find` — Search for Files

The `find` command searches for files and directories based on specified criteria.

### Find a Specific File

```bash
find -name passwords.txt
```

**Output**

```text
./folder1/passwords.txt
```

---

### Find All Text Files

Wildcards (`*`) can be used to match multiple filenames.

```bash
find -name "*.txt"
```

**Output**

```text
./folder1/passwords.txt
./Documents/todo.txt
```

### Tip

The `*` wildcard matches any sequence of characters.

Examples:

```bash
find -name "*.log"
find -name "*.conf"
find -name "*.txt"
```

---

## `grep` — Search Inside Files

The `grep` command searches the contents of a file for matching text.

### Search for an IP Address

```bash
grep "81.143.211.90" access.log
```

**Output**

```text
81.143.211.90 - - [25/Mar/2021:11:17 +0000] "GET / HTTP/1.1" 200 417 "-" "Mozilla/5.0 (Linux; Android 7.0; Moto G(4))"
```

### Practical Uses

- Searching log files
- Finding usernames
- Locating IP addresses
- Identifying error messages
- Searching for flags during CTF challenges

---

## `grep -R` — Recursive Search

The `-R` option tells `grep` to search through every file inside a directory and its subdirectories.

### Example

```bash
grep -R "PRETTY_NAME" /etc/
```

**Example Output**

```text
grep: /etc/sudoers: Permission denied
/etc/os-release:PRETTY_NAME="Ubuntu"
```

This command displays both the matching line and the file in which it was found.

---

## `wc -l` — Count Lines

The `wc` (word count) command can count lines, words, or characters.

Using the `-l` option counts the number of lines in a file.

### Example

```bash
wc -l access.log
```

**Output**

```text
244 access.log
```

This is useful for estimating the size of log files before analyzing them.

---

## Cybersecurity Relevance

Searching efficiently is a fundamental cybersecurity skill.

Security professionals use these commands to:

- Locate configuration files.
- Search web server logs for suspicious activity.
- Find Indicators of Compromise (IOCs).
- Search for credentials or API keys.
- Locate flags during Capture The Flag (CTF) exercises.
- Perform digital forensics and incident response investigations.

---

## Key Takeaways

- `find` searches for files and directories.
- Wildcards (`*`) make searches more flexible.
- `grep` searches file contents for specific text.
- `grep -R` performs recursive searches across directories.
- `wc -l` counts the number of lines in a file.
- These commands are essential for Linux administration, penetration testing, and cybersecurity.


---

# 4. Shell Operators

## Overview

Shell operators allow users to perform more advanced actions when executing commands in the Linux terminal. They can be used to run commands in the background, chain multiple commands together, or redirect command output to files.

These operators improve efficiency and are commonly used in Linux administration, automation, and cybersecurity tasks.

---

## Operators Learned

| Operator | Description |
|----------|-------------|
| `&` | Runs a command in the background. |
| `&&` | Executes the next command only if the previous command succeeds. |
| `>` | Redirects output to a file, overwriting existing contents. |
| `>>` | Appends output to a file without overwriting existing contents. |

---

## `&` — Run a Command in the Background

The `&` operator executes a command in the background, allowing you to continue using the terminal while the command is still running.

### Example

```bash
long_running_command &
```

### Practical Use

This operator is useful when:

- Copying large files
- Running scripts
- Executing long-running processes
- Keeping the terminal available for other tasks

---

## `&&` — Execute Commands Sequentially

The `&&` operator connects two commands.

The second command is executed **only if the first command completes successfully**.

### Example

```bash
mkdir test && cd test
```

**Explanation**

1. Create a directory named `test`.
2. If the directory is created successfully, change into it.

---

## `>` — Redirect Output (Overwrite)

The `>` operator redirects command output to a file.

If the file does not exist, it is created.

If the file already exists, **its contents are replaced**.

### Example

```bash
echo hey > welcome
```

### Before

```text
(empty file)
```

### After

```text
hey
```

### Important

Running another command with `>` replaces the existing content.

```bash
echo hello > welcome
```

**Result**

```text
hello
```

The previous content (`hey`) is overwritten.

---

## `>>` — Append Output

The `>>` operator also redirects output to a file.

Unlike `>`, it **adds new content to the end of the file** without deleting the existing content.

### Example

```bash
echo hello >> welcome
```

### Before

```text
hey
```

### After

```text
hey
hello
```

If the file does not exist, Linux creates it automatically.

---

## Cybersecurity Relevance

Shell operators are frequently used by system administrators and cybersecurity professionals.

Common use cases include:

- Saving command output to log files.
- Combining multiple commands during system administration.
- Running long-running security scans in the background.
- Redirecting scan results for later analysis.
- Automating repetitive tasks with shell scripts.

Examples include saving the output of tools like `nmap`, `find`, or `grep` into files for reporting or investigation.

---

## Key Takeaways

- `&` runs a command in the background.
- `&&` executes the next command only if the previous one succeeds.
- `>` redirects output and overwrites existing content.
- `>>` appends output without removing existing content.
- Shell operators make command-line workflows more efficient and are widely used in Linux administration and cybersecurity.

---

## Skills Acquired

After completing this room, I gained hands-on experience with:

- Linux terminal basics
- Command-line navigation
- Filesystem management
- File searching with `find`
- Text searching with `grep`
- Counting file lines with `wc`
- Shell operators (`&`, `&&`, `>`, `>>`)
- Output redirection
- Basic Linux command-line workflow

---

## Next Steps

Continue learning:

- Linux Fundamentals Part 2
- Linux file permissions
- SSH
- Package management
- User and group management
- Bash scripting
