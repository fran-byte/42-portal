---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Prerequisites (before tackling get_next_line)

### 📌 Objective:

Understand how **file reading works in C** using `read`, how to manage buffers, dynamically concatenate strings, and control memory with `malloc` and `free`, to build a robust function capable of **reading line by line** from a file descriptor.

---

### 📁 What is `get_next_line`?

It’s a function that reads from a file descriptor line by line and returns each line ending in `\n`. You must implement it **without using forbidden libc functions** (like `strdup`, `strjoin`, etc.).

---

### 🔧 How do you use it?

```c
char *line;

line = get_next_line(fd);
while (line != NULL)
{
    printf("%s", line);
    free(line);
    line = get_next_line(fd);
}
```

---

### 🧠 Key concepts before starting

#### ✅ File descriptor (`fd`)

A **file descriptor** is an integer that represents an open file. For example:

* `0`: stdin
* `1`: stdout
* `2`: stderr
* `fd = open("file.txt", O_RDONLY);`

---

#### ✅ The `read` function

`read(fd, buffer, BUFFER_SIZE)` reads up to `BUFFER_SIZE` bytes from `fd` into `buffer`. It returns:

* The number of bytes read
* `0` if it reaches the end of file (EOF)
* `-1` in case of error

---

### 📦 What should you implement?

#### 🧾 Mandatory prototype:

```c
char *get_next_line(int fd);
```

In addition, you may (and should) create helper functions in separate files like:

* `ft_strjoin`
* `ft_strchr`
* `ft_strlen`
* `ft_strdup`
* `ft_substr`

---

### 🧱 Minimal project structure

```
get_next_line/
├── get_next_line.c
├── get_next_line.h
├── get_next_line_utils.c
├── main.c (for testing)
```

---

### ⚙️ BUFFER_SIZE

You must compile your project in a way that allows the evaluator to define `BUFFER_SIZE`:

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 main.c get_next_line.c get_next_line_utils.c
```

> ✅ Use `#ifndef BUFFER_SIZE` in your `.h` file to set a default value if one is not provided at compile time.

---

### 🧩 Technical tips for implementing `get_next_line`

* Use a **static buffer** or `static char *leftover` to store what's left between function calls.
* Concatenate what you read until you find a `\n`.
* Once a full line is found, **separate the line from what remains**.
* At end of file, return whatever is left in the buffer.

---

### 📚 Useful resources

* `man 2 read`
* `man open`, `man close`
* `valgrind` to detect memory leaks
* `strchr`, `strjoin`, `strdup`, `strlen`, `substr` — if you can’t use them, **reimplement them yourself**.

---

### 🧠 Practical advice

* Start by implementing a version **without static buffers**, to understand the logic.
* Then add static buffer handling for multiple calls.
* Test with large files and lines that **don’t end in `\n`**.
* Use `valgrind` to ensure you have **no memory leaks**.
* Split your code into functions by responsibility: one to find the newline, one to split strings, one to clean memory.

---
