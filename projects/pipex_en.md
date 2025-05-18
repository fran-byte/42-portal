---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Prerequisites (Before Starting pipex)

### 📌 Objective:

Recreate the behavior of **shell pipes (`|`) and input/output redirections**, using system calls in C. Your program must **execute two commands in sequence**, redirecting input and output to files, and **connecting them via a pipe**.

---

## 🔧 What Does `pipex` Do?

It executes two chained commands, managing their input/output flow:

```bash
./pipex infile cmd1 cmd2 outfile
````

This is equivalent to the shell command:

```bash
< infile cmd1 | cmd2 > outfile
```

📌 That is:

* The input for `cmd1` comes from a file.
* Its output is piped to `cmd2`.
* The final output is redirected to another file.

---

## 🔁 Program Execution Flow

1. Open `infile` and redirect it as `stdin` of `cmd1`.
2. Create a pipe to connect `cmd1` and `cmd2`.
3. Redirect the `stdout` of `cmd1` to the write-end of the pipe.
4. Redirect the `stdin` of `cmd2` to the read-end of the pipe.
5. Open `outfile` and redirect `stdout` of `cmd2` to it.

📌 Each step is done in a child process created with `fork()`.

---

## 🧠 Key System Functions

| Function   | Description                                                     |
| ---------- | --------------------------------------------------------------- |
| `pipe()`   | Creates a communication channel (pipe) between two processes.   |
| `fork()`   | Creates a child process to run a command.                       |
| `dup2()`   | Redirects `stdin` or `stdout` to a file descriptor or pipe end. |
| `execve()` | Executes the given command, replacing the current process.      |
| `open()`   | Opens files for reading or writing.                             |
| `close()`  | Closes unused file descriptors.                                 |
| `wait()`   | Waits for child processes to finish to avoid zombie processes.  |

---

## 📦 PATH Lookup (Command Resolution)

To run a command like `"ls"` or `"grep"`, you must find the full path to the executable using the `PATH` environment variable.

### 🔍 How It Works:

1. Retrieve `PATH` from `envp[]`.
2. Split it by `:` to get directories.
3. Concatenate each directory with the command name.
4. Use `access(path, X_OK)` to check if it’s executable.
5. Pass the full path to `execve()`.

---

## 🧪 Example Usage

```bash
./pipex input.txt "grep hello" "wc -l" output.txt
```

Shell equivalent:

```bash
< input.txt grep hello | wc -l > output.txt
```

✅ Flow:

1. `input.txt` → `stdin` of `grep hello`
2. `stdout` of `grep hello` → `stdin` of `wc -l` (via pipe)
3. `stdout` of `wc -l` → `output.txt`

---

## ⚙️ Flow Diagram

![pipex flow diagram](../../img/milestone_2/pipex_flujo.png)

---

## 📉 Common Pitfalls

1. ❌ **Unclosed descriptors**: may cause deadlocks or resource leaks.
2. 🔐 **File permission errors**: always check read/write access before opening.
3. 🚫 **System call errors**: use `perror()` or `strerror(errno)` for debugging.

---

## 🛠️ Allowed Functions

You may use:

* `open`, `close`, `read`, `write`, `malloc`, `free`, `perror`, `strerror`
* `access`, `dup`, `dup2`, `execve`, `exit`, `fork`, `pipe`, `unlink`, `wait`, `waitpid`
* Your own implementation of `ft_printf` (or equivalent) if needed

---

## 🧱 Minimal Project Structure

```
pipex/
├── pipex.c
├── pipex.h
├── path_utils.c
├── exec_utils.c
├── error_handling.c
├── main.c
```

---

## 📚 Useful Resources

* [`man 2 pipe`](https://man7.org/linux/man-pages/man2/pipe.2.html)
* [`man 2 execve`](https://man7.org/linux/man-pages/man2/execve.2.html)
* [`man 3 access`](https://man7.org/linux/man-pages/man3/access.3p.html)
* [C pipes explained (PDF)](https://www.cs.buap.mx/~hilario_sm/slide/SO-1/Pipe.pdf)

---

## 🧠 Practical Tips

* ✨ Start with just one command working before introducing `fork()`.
* 💡 Create a dedicated function for `PATH` resolution.
* 🧪 Test with real files and broken commands to handle edge cases.
* 🧼 Free all allocated memory and close all file descriptors. Use `valgrind`.
* 📦 Validate input: correct number of arguments, file existence, permissions.

---
