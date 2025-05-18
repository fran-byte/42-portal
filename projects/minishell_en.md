---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Prerequisites (Before Starting Minishell)

### 📌 Objective:

The **Minishell** project aims to implement a mini command-line interface (shell) capable of executing commands like a real Unix shell, with support for pipes, redirections, environment variables, and signal handling. You will develop a deep understanding of how shells behave and how system calls work in Linux.

---

## 🔹 2. Expected Behavior

### 🚀 Your minishell should be able to:

* Display a prompt and wait for commands.
* Execute commands with arguments.
* Support redirections: `>`, `>>`, `<`, `<<`.
* Execute piped commands: `ls | grep txt`.
* Handle single and double quotes correctly.
* Manage environment variables: `$USER`, `$PATH`, etc.
* Implement built-in commands like `cd`, `echo`, `pwd`, `export`, `unset`, `env`, `exit`.
* Handle `Ctrl+C`, `Ctrl+D`, and `Ctrl+\` (interrupt signals).

---

## 🪧 3. Key Functions and Concepts

| Function                 | Main Use                               |
| ------------------------ | -------------------------------------- |
| `fork()`                 | Create a child process                 |
| `execve()`               | Replace the process with a new one     |
| `pipe()`                 | Create communication between processes |
| `dup2()`                 | Redirect file descriptors              |
| `waitpid()`              | Wait for a child process to finish     |
| `read()`/`write()`       | Read and write to files or descriptors |
| `open()`                 | Open files with mode flags             |
| `close()`                | Close descriptors                      |
| `signal()`/`sigaction()` | Handle system signals                  |
| `getenv()`               | Get environment variables              |
| `setenv()`/`unsetenv()`  | Set/remove environment variables       |

---

## 📃 4. Project Structure

```
minishell/
├── minishell.c         // Main loop and parsing
├── parser.c            // Command parsing, tokens, quotes
├── executor.c          // Command execution and redirections
├── builtin.c           // Built-in command implementations
├── signals.c           // Signal handling
├── env.c               // Environment variable handling
├── utils/              // Common utilities
├── includes/           // Header files
```

---

## 📈 5. Signal Management

Your minishell should:

* Ignore `Ctrl+\` (`SIGQUIT`) when no command is running.
* Handle `Ctrl+C` (`SIGINT`) to cancel the current command and show a new prompt.
* Handle `Ctrl+D` (EOF) properly: exit if the prompt is empty.

---

## 🔍 6. Redirections

| Redirection | Meaning                                           |
| ----------- | ------------------------------------------------- |
| `>`         | Redirects stdout to a file (overwrite)            |
| `>>`        | Redirects stdout to a file (append)               |
| `<`         | Redirects stdin from a file                       |
| `<<`        | Here-document: stdin from a delimited input block |

---

## 🤖 7. Environment Variables

### Implement support for:

* Variable expansion with `$NAME`.
* Export new variables with `export`.
* Remove variables with `unset`.
* List variables with `env`.

---

## 🚛 8. Execution Example

```bash
$ echo "Hello world"
Hello world

$ export USERNAME=fran
$ echo $USERNAME
fran

$ cat << EOF
> line 1
> line 2
> EOF
line 1
line 2

$ ls | grep .c > files.txt
```

---

## 🚧 9. Built-in Commands

* `cd [path]`
* `pwd`
* `echo [args]`
* `export VAR=value`
* `unset VAR`
* `env`
* `exit`

---

## 📊 10. Practical Tips

* Use structures to represent commands, tokens, redirections.
* Implement robust parsing (quotes, escapes, pipes, multiple redirs).
* Start with simple commands, then add more features.
* Test memory issues using Valgrind:

```bash
valgrind --leak-check=full ./minishell
```

---

## 📅 11. Useful Resources

* `man 3 getenv`, `man 2 execve`, `man 2 pipe`, `man 2 dup2`
* [GNU Bash Manual](https://www.gnu.org/software/bash/manual/bash.html)
* [Shell Command Language (POSIX)](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html)

---
