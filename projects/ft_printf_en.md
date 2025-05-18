---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Prerequisites (Before Starting ft_printf)

### 📌 Objective:

To understand how **formatted output works in C**, using `write`, variadic functions (`va_list`), and type conversion logic, in order to build your own version of the `printf` function that correctly handles various data types.

---

### 🧠 Key Concepts Before You Begin

#### ✅ `write(int fd, const void *buf, size_t count)`

This is the basic function you'll use to print output:

```c
write(1, &c, 1);  // prints a single character
````

#### ✅ `va_list` (Variadic Functions)

Here is the full English translation of the paragraph you provided:

---

To handle variable arguments (`...`), we need to use macros from the `<stdarg.h>` header:

```c
#include <stdarg.h>

va_list args;
va_start(args, format);
... // va_arg(args, type)
va_end(args);
```

* **`va_list`**: Declares a variable that holds information about the additional arguments.
* **`va_start`**: Initializes the `va_list` variable with the variable arguments.
* **`va_arg`**: Used to retrieve each argument from the list.
* **`va_end`**: Cleans up the list once all arguments have been processed.


---

### 💡 **TIP — How Variadic Functions Work**

Functions with `...` (like `ft_printf`) **don’t know how many arguments are passed or their types**. You must handle them one by one using macros from `stdarg.h`:

```c
va_list args;
va_start(args, format);      // Start reading arguments
int n = va_arg(args, int);   // Retrieve the next argument as int
va_end(args);                // Clean up
```

> ⚠️ The extraction order must **exactly match the format string**. If you read a `char *` when the next value is an `int`, you’ll get undefined behavior.

---

### 🖨️ What is `ft_printf`?

It’s a reimplementation of the standard `printf` function in C, which displays formatted data to the standard output.

Your version should behave like `printf` but only support a **limited set of format specifiers** as defined in the subject (such as `%c`, `%s`, `%d`, `%x`, etc.).

---

### 🔧 How Is It Used?

```c
ft_printf("Character: %c\n", 'A');
ft_printf("String: %s\n", "Hello");
ft_printf("Number: %d\n", 42);
ft_printf("Hex: %x\n", 255);
```

> ✅ It must return the **total number of characters printed**, just like the original `printf`.

---

### 📦 What Do You Need to Implement?

#### 🧾 Required Prototype:

```c
int ft_printf(const char *format, ...);
```

#### 🎯 Required Format Specifiers:

| Specifier   | Meaning                   |
| ----------- | ------------------------- |
| `%c`        | Character                 |
| `%s`        | String                    |
| `%p`        | Pointer address           |
| `%d` / `%i` | Signed integer            |
| `%u`        | Unsigned integer          |
| `%x` / `%X` | Hexadecimal (lower/upper) |
| `%%`        | Literal percent sign      |

---

### 🧱 Minimal Project Structure

```
ft_printf/
├── ft_printf.c
├── ft_printf.h
├── ft_utils.c
├── main.c (for testing)
```

---

### ⚙️ Recommended Compilation

```bash
cc -Wall -Wextra -Werror ft_printf.c ft_utils.c main.c
```

> ❗ Do not use forbidden functions like `printf`, `itoa`, `sprintf`, etc.

---

### 🧩 Technical Tips for Implementing `ft_printf`

* **Divide and conquer**: create a function for each format type.

* Use `va_arg` to retrieve each dynamic argument.

* Write your own versions of:

  * `ft_strlen`
  * `ft_putnbr`
  * `ft_putstr`
  * `ft_itoa_base` for hexadecimal

* Use counters to keep track of the number of printed characters.

* Handle pointer formatting (`%p`) by converting to hexadecimal and prepending `0x`.

---

### 📚 Useful Resources

* `man 3 printf`
* `man 2 write`
* `man stdarg`
* [cppreference.com — printf specification](https://en.cppreference.com/w/c/io/fprintf)

---

### 🧠 Practical Advice

* Start by implementing `%c`, `%s`, and `%%` to get the structure right.
* Carefully count the characters printed — it's what your function must return.
* Use `valgrind` to check for memory leaks, especially with `%p` and strings.
* Test each format type with edge cases (e.g., NULL strings, negative numbers, large hex values).
* Use a switch statement or a table to dispatch the format handlers efficiently.

---
