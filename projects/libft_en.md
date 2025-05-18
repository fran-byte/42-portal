---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Prerequisites (Before Starting Libft)

### 📌 Goal:

To have **all the technical and conceptual tools** you need to start Libft **with confidence**, avoiding common mistakes and fully understanding **what you're doing and why**.

---

### 🛠️ How to Compile in C (`gcc`, flags, `Makefile`)

#### ✅ What does it mean to compile?

It's the process of transforming your `.c` source code into **executable machine code**. The most commonly used compiler at 42 is `cc`.

#### 🔧 What is `cc` and how do you use it?

```bash
gcc -Wall -Wextra -Werror file.c -o executable

# Or we can use gcc if our project allows it:

gcc -Wall -Wextra -Werror file.c -o executable

```

* **`-Wall`**: enables all standard warnings.
* **`-Wextra`**: enables additional warnings.
* **`-Werror`**: treats all warnings as errors (forcing clean code).
* **`-o`**: specifies the name of the resulting executable.

> ⚠️ In 42 projects, **these flags are mandatory**, and your code must compile **without any warnings**.

---

#### 🧱 What is a Makefile?

A **Makefile** is a script that automates the compilation process. Instead of typing multiple commands by hand, you define rules that handle them for you. It's required in Libft.

#### 🧪 Basic Makefile Example for Libft:

```make
NAME = libft.a
SRC = ft_strlen.c ft_isalpha.c
OBJ = $(SRC:.c=.o)

CC = cc
CFLAGS = -Wall -Wextra -Werror

all: $(NAME)

$(NAME): $(OBJ)
	ar rcs $(NAME) $(OBJ)

clean:
	rm -f $(OBJ)

fclean: clean
	rm -f $(NAME)

re: fclean all

.PHONY: all clean fclean re
```

* **`ar rcs`**: creates the static library (`.a`)
* **Required rules**: `all`, `clean`, `fclean`, `re`, and `$(NAME)`
* **No relinking**: make sure you don’t compile more times than needed

---

### 📦 What Is a Static Library (`.a`)?

A **static library** is a file that **contains precompiled code**, ready to be reused. Instead of copying functions into every new project, you just link your `libft.a`.

#### 📌 How to use it:

1. Create the library:

```bash
ar rcs libft.a ft_strlen.o ft_isalpha.o ...
```

2. Use it like this:

```bash
gcc main.c -L. -lft -o program
```

* `-L.` tells gcc to look for libraries in the current directory
* `-lft` searches for `libft.a` (dropping the `lib` prefix and `.a` extension)

---

### 📚 Using `man` and Official Documentation

#### ✅ What is `man`?

`man` stands for "manual". It shows the official documentation for system functions.

Example:

```bash
man strlen
```

This shows:

* The prototype: `size_t strlen(const char *s);`
* What it does: counts characters until `\0`
* What it returns: a number (`size_t`)
* Possible errors: in this case, none

#### 🧠 Why is this critical at 42?

You are required to **re-implement standard library functions**, like `memcpy`, `strchr`, etc. The `man` pages are the official source that describes **exactly** how these functions behave.

---

### 🧬 Anatomy of a Function in C

Let’s break down a function step by step:

```c
int ft_strlen(const char *s)
{
    int i = 0;
    while (s[i])
        i++;
    return i;
}
```

#### Key elements:

* `int`: return type. The function returns an integer.
* `ft_strlen`: function name. All your functions must start with `ft_`.
* `const char *s`: input parameter. This is a string that you **won’t modify**.
* `{ ... }`: the function body.
* `while (s[i])`: loops through the string until it finds `\0`.
* `return i`: returns the length.

> ✨ Pro tip: before writing code, **think through the logic in plain English or pseudocode**.

---

### 🧾 Standard Data Types

| Type     | Meaning                               | Example               |
| -------- | ------------------------------------- | --------------------- |
| `int`    | Integer (positive or negative)        | `int x = -42;`        |
| `char`   | Character (letter, number, symbol)    | `char c = 'A';`       |
| `void`   | No type / returns nothing             | `void ft_print(void)` |
| `size_t` | Unsigned size (used in strings, etc.) | `size_t len = 5;`     |

#### 📌 What is `size_t`?

It’s an **unsigned type** used for memory sizes and array lengths.

Example:

```c
size_t ft_strlen(const char *s);
```

Using it avoids negative values and ensures compatibility across platforms (32-bit, 64-bit).

---

### 🔗 Pointers and Basic Arrays

#### ✅ What is a pointer?

A pointer is a variable that **stores the memory address of another variable**.

```c
int x = 10;
int *p = &x;  // p points to x
```

You can access the value of `x` through the pointer:

```c
printf("%d\n", *p);  // prints 10
```

---

#### ✅ What is an array?

An array is a **collection of elements of the same type stored contiguously in memory**.

```c
char greeting[] = "Hello";
```

This is almost the same as:

```c
char *greeting = "Hello";
```

In both cases, `greeting[0]` is `'H'`, `greeting[1]` is `'e'`, etc.

---

#### 📌 Relevance to Libft:

Many Libft functions use pointers:

* `const char *s` → points to the start of a string
* `char *dst, const char *src` → used for copying data
* `void *b` → used in generic functions like `memset`

> Understanding how pointers and arrays work is **crucial** to avoid common issues like segfaults or buffer overflows.

---

### 🧠 Practical Tips

* **Write small tests in separate files** before integrating them into your Libft.
* Use `valgrind` to detect memory issues (especially when you start using `malloc`).
* Read the `man` page before starting any function, **even if you think you know what it does**.
* Start with **simple functions** (like `ft_isalpha`) to get comfortable.
* Use `printf` for debugging. Don’t hesitate to print values to understand what’s happening.

---
