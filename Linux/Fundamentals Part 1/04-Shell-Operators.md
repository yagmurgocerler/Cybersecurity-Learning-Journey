# Shell Operators

## Overview

In this section, I learned how shell operators can make working with Linux more efficient by combining commands, running tasks in the background, and redirecting output.

---

## Operators Learned

### `&`

Runs a command in the background.

```bash
command &
```

Example:

```bash
cp largefile.txt backup.txt &
```

---

### `&&`

Runs multiple commands in sequence. The second command only executes if the first one succeeds.

```bash
command1 && command2
```

Example:

```bash
mkdir test && cd test
```

---

### `>`

Redirects the output of a command to a file.

If the file already exists, its contents will be overwritten.

```bash
echo hey > welcome
```

Example Output:

```
welcome
└── hey
```

---

### `>>`

Appends the output of a command to the end of a file without overwriting the existing contents.

```bash
echo hello >> welcome
```

Example Output:

```
hey
hello
```

---

## Key Concepts

- `&` runs commands in the background.
- `&&` chains commands together and only continues if the previous command succeeds.
- `>` redirects and overwrites file contents.
- `>>` appends data to a file without removing existing content.

---

## Skills Gained

- Running background processes
- Combining multiple commands
- Redirecting command output
- Appending data to files
- Understanding shell operators
