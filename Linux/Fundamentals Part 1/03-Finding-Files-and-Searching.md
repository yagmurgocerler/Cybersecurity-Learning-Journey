# Finding Files and Searching

## Overview

In this section, I learned how to search for files and find specific information inside files using Linux commands. These commands are extremely useful for system administration and cybersecurity tasks.

---

## Commands Learned

### `find`

Searches for files and directories.

Find a specific file:

```bash
find -name passwords.txt
```

Find all text files:

```bash
find -name "*.txt"
```

Example Output:

```
./folder1/passwords.txt
./Documents/todo.txt
```

---

### `grep`

Searches for a specific word or pattern inside a file.

```bash
grep "81.143.211.90" access.log
```

Example Output:

```
81.143.211.90 - - [25/Mar/2021:11:17 +0000] "GET / HTTP/1.1"
```

---

### Recursive Search with `grep`

Search inside all files and subdirectories.

```bash
grep -R "PRETTY_NAME" /etc/
```

Example Output:

```
/etc/os-release:PRETTY_NAME="Ubuntu"
```

---

### `wc`

Counts lines, words, or characters in a file.

Count the number of lines:

```bash
wc -l access.log
```

Example Output:

```
244 access.log
```

---

## Key Concepts

- Use `find` to locate files and directories.
- Wildcards (`*`) can search for files with a specific extension.
- `grep` searches for text inside files.
- `grep -R` performs recursive searches in directories.
- `wc -l` counts the number of lines in a file.

---

## Skills Gained

- Searching for files with `find`
- Using wildcards (`*`)
- Searching text inside files with `grep`
- Recursive searching using `grep -R`
- Counting file lines with `wc`
