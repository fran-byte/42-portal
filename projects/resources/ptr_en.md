---
layout: default
title: "fran-byte 42 Madrid — Pointers in C"
---

## 🔹 Pointers in C – Support Resource for Libft

### 📌 Objective

Deepen your understanding of pointers in C: memory access, data manipulation, arrays, structures, casting, and dynamic memory. This resource complements your learning for tackling projects like **Libft** or **get\_next\_line**.

---

## 1️⃣ What is a pointer?

A **pointer** is a variable that stores the **memory address** of another variable. In C, each variable occupies a specific memory location, and pointers let you directly access those locations, optimizing performance and enabling dynamic data management.

```c
int *p; // Pointer to an integer
char *q; // Pointer to a character
```

A pointer that doesn't point to a valid memory address is considered "dead" or null (`NULL`).

---

## 2️⃣ Operators: Reference and Dereference

* `&`: gets the memory address of a variable.
* `*`: accesses the value at the memory address (dereference).

```c
int x = 10;
int *p = &x;

printf("%d\n", x);   // 10
printf("%p\n", &x);  // Address of x
printf("%p\n", p);   // Address of x (same as &x)
printf("%d\n", *p);  // 10
```

---

## 3️⃣ Indirect Modification with Pointers

```c
int x = 20;
int *p = &x;
*p = 50;
printf("%d\n", x); // 50
```

---

## 4️⃣ Pointers and Arrays

Arrays in C act as pointers to the first element:

```c
int arr[] = {10, 20, 30};
int *p = arr;

for (int i = 0; i < 3; i++)
    printf("%d\n", *(p + i));
```

This is equivalent to `arr[i]`. That's also why you can pass arrays to functions as pointers.

---

## 5️⃣ Pointers to Pointers

You can have pointers that point to other pointers:

```c
int x = 100;
int *p = &x;
int **pp = &p;

printf("%d\n", **pp); // 100
```

These levels of indirection are useful in structures like linked lists.

---

## 6️⃣ Swapping Values Using Pointers

```c
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

Usage:

```c
int x = 5, y = 10;
swap(&x, &y);
```

---

## 7️⃣ Casting (Type Casting)

```c
int a = 5, b = 2;
float result = (float)a / b; // 2.5
```

Without casting, the result would be `2` (integer). Casting converts the type to ensure the desired result.

---

## 8️⃣ `malloc` and Dynamic Memory

`malloc` returns a `void *`, which you must cast to the correct type:

```c
int *ptr = (int *)malloc(sizeof(int));
*ptr = 10;
free(ptr);
```

### 📌 Why cast?

```c
struct node *n = (struct node *)malloc(sizeof(struct node));
```

* `malloc` doesn’t know the type, so you cast to clarify.

---

## 9️⃣ Full Example with `malloc`

```c
int *ptr = (int *)malloc(sizeof(int));
if (ptr == NULL) return 1;
*ptr = 25;
printf("Value: %d\n", *ptr);
free(ptr);
```

---

## 🔟 Pointers and Structures (`->`)

```c
struct employee {
    char name[20];
    float salary;
};

struct employee data = {"John", 3500.50};
struct employee *emp = &data;
printf("Name: %s\n", emp->name);
printf("Salary: %.2f\n", emp->salary);
```

---

## ✅ Summary

* `*` dereferences, `&` gets address
* Arrays and pointers are equivalent in many cases
* Pointers allow you to modify values and manage dynamic structures
* `malloc` allocates memory, `free` deallocates it
* `->` accesses struct members via a pointer

---

## 📚 Recommended Resources

* `man malloc`, `man pointer`, `man struct`
* [cplusplus.com - pointers](https://cplusplus.com/doc/tutorial/pointers/)
* [Valgrind - Memory Error Detection](https://valgrind.org/)

---
