---
layout: default
title: "fran-byte 42 Madrid"
---

# Part 1 - libc functions


## [ft_isalpha](../0/libft/ft_isalpha.c)

``` c
int ft_isalpha (int c)
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
Checks if it is an **alphabetic** character. | The character to test | 0 if the character is false and 1 if the character is true

## [ft_isdigit](../0/libft/ft_isdigit.c)

``` c
int ft_isdigit (int c)
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
Check if it is a **digit** (0 to 9) | The character to test | 0 if the character is false and 1 if the character is true

## [ft_isalnum](../0/libft/ft_isalnum.c)

``` c
int ft_isalnum (int c)
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
Checks if it is an **alphanumeric** character. | The character to test | 0 if the character is false and 1 if the character is true

## [ft_isascii](../0/libft/ft_isascii.c)

``` c
int ft_isascii (int c)
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
Checks if it is an **ASCII** character, which is any character between 0 and octal 0177 inclusive | The character to test | 0 if the character is false and 1 if the character is true

## [ft_isprint](../0/libft/ft_isprint.c)

``` c
int ft_isprint (int c)
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
Check if it is a **printable** character, including space | The character to test | 0 if the character is false and 1 if the character is true

## [ft_strlen](../0/libft/ft_strlen.c)
``` c
size_t ft_strlen (const char *s)
```

Description | Param. #1 | Valores de Retorno
:-----------: | :-----------: | :-----------:
Calculates the **length** of the string pointed to by "s", excluding the terminating null byte ('\0') | The string to calculate | Number of characters in the string pointed to by "s"

## [ft_memset](../0/libft/ft_memset.c)

``` c
void *ft_memset (void *s, int c, size_t len)
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Fill** "s" memory with "len" bytes of "c" | The string to operate on | Value c (converted to unsigned char) | The number of bytes | A pointer to the memory area s

## [ft_bzero](../0/libft/ft_bzero.c)

``` c
void *ft_bzero (void *s,  size_t n)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Erases** the data in "n" bytes of memory starting at the location pointed to by "s", writing zeros | The string to operate on | The number of bytes | None

## [ft_memcpy](../0/libft/ft_memcpy.c)

``` c
void *ft_memcpy (void *dst, const void *src, size_t n)
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Copy** "n" bytes from memory area "src" to memory area "dst". Memory areas must not overlap (If dst size is less than n) **may overwrite adjacent memory**. Use [ft_memmove](#ft_memmove) if memory areas overlap. | dst memory area | src memory area | The number of bytes | A pointer to the dst memory area

## [ft_memmove](../0/libft/ft_memmove.c)

``` c
void *ft_memmove (void *dst, const void *src, size_t len)
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Copy** "len" bytes from memory "src" to "dst". Memories may overlap. First, bytes in "src" are copied to a temporary array and then to "dst". (If size of dst is less than n) **may overwrite adjacent memory** | dst memory area | src memory area | The number of bytes | A pointer to the dst memory area

## [ft_strlcpy](../0/libft/ft_strlcpy.c)

``` c
size_t ft_strlcpy (char *dst, const char *src, size_t dstsize)
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Copy** up to "dstsize - 1" characters from the NUL-terminated string "src" to "dst", NUL-terminating the result | Destination array | String to copy | Number of characters to copy from "src" | Total length of the created string (length of "src")

## [ft_strlcat](../0/libft/ft_strlcat.c)

``` c
size_t ft_strlcat (char *dst, const char *src, size_t size)
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Concatenate** the string "src" to the end of "dst". Will concatenate at most "size - strlen(dst) - 1" bytes, NUL terminating the result | Destination array | String to append to "dst" | Maximum number of characters to append | The initial length of "dst" plus the length of "src"

## [ft_toupper](../0/libft/ft_toupper.c)

``` c
int ft_toupper (int c)
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
If the character passed as an argument is a lowercase letter, it is converted to **uppercase** | The character to convert | If "c" is a lowercase letter, it returns its uppercase equivalent. Otherwise, it returns "c"

## [ft_tolower](../0/libft/ft_tolower.c)

``` c
int ft_tolower (int c)
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
If the character passed as an argument is an uppercase letter, it is converted to **lowercase** | The character to convert | If "c" is an uppercase letter, it returns its lowercase equivalent. Otherwise, it returns "c"

## [ft_strchr](../0/libft/ft_strchr.c)

``` c
char *ft_strchr (const char *s, int c)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
Locates the **first** occurrence of "c" in the string pointed to by "s". The terminating null character is considered part of the string, so if "c" is '\0', locate the final '\0' | Pointer to string | Character to locate | A pointer to the first occurrence of the character "c" in the string or NULL if the character is not found

## [ft_strrchr](../0/libft/ft_strrchr.c)

``` c
char *ft_strrchr (const char *s, int c)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
Locates the **last** occurrence of "c" in the string pointed to by "s". The terminating null character is considered part of the string, so if "c" is '\0', locate the final '\0' | Pointer to string | Character to locate | A pointer to the last occurrence of the character "c" in the string or NULL if the character is not found

## [ft_strncmp](../0/libft/ft_strncmp.c)

``` c
int ft_strncmp (const char *s1, const char *s2, size_t n)
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Compare** the first "n" bytes of strings "s1" and "s2". | String 1 to compare | String 2 to compare | The number of bytes to compare | A negative, zero, or positive integer, depending on whether "s1" is less than, equal to, or greater than "s2".

## [ft_memchr](../0/libft/ft_memchr.c)

``` c
void *ft_memchr (const void *s, int c, size_t n)
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Scan** the first "n" bytes of "s" looking for the first instance of "c" | Memory area s | A character to search for | The number of bytes | A pointer to the matching byte or NULL if the character does not appear in the given memory area

## [ft_memcmp](../0/libft/ft_memcmp.c)

``` c
void *ft_memcmp (void *dst, const void *src, size_t n)
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Compare** byte string "s1" with byte string "s2" | Memory area s1 | Memory area s2 | Number of bytes | < 0 if s1 is less than s2, > 0 if s1 is greater than s2, = 0 if s1 is equal to s2

## [ft_strnstr](../0/libft/ft_strnstr.c)

``` c
char *ft_strnstr (const char *haystack, const char *needle, size_t len)`
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Find** a substring, where no more than "len" characters are searched. Find the first occurrence of the substring "needle" in the string "haystack". Terminating null bytes ('\0') are not matched | String to search for | The substring to search for in "haystack" | The maximum number of characters to search for | A pointer to the first character of the first occurrence of "needle". NULL if the substring is not found. If "needle" is an empty string, "haystack" is returned

## [ft_atoi](../0/libft/ft_atoi.c)

``` c
int ft_atoi (const char *str)
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
**Convert** a string to an integer | The string to convert to an integer | The converted value


## [ft_calloc](../0/libft/ft_calloc.c)

``` c
void *ft_calloc (size_t count, size_t size)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Allocates** enough space for "count" objects, each of "size" bytes of memory, and returns a pointer to the allocated memory. The allocated memory is filled with bytes of value zero | Number of items to allocate | Size of items | A pointer to the allocated memory, or NULL if the request fails


## [ft_strdup](../0/libft/ft_strdup.c)

``` c
char *ft_strdup (const char *s)`
```

Description | Param. #1 | Valores de Retorno
:-----------: | :-----------: | :-----------:
**Duplicates** the string "s". Memory for the new string is obtained with malloc and can be freed with free | The string to duplicate | A pointer to the duplicated string. NULL if there was not enough memory available

<br><br><br><br><br>

# Part 2 - Additional Features

## [ft_substr](../0/libft/ft_substr.c)

``` c
char *ft_substr (char const *s, unsigned int start, size_t len)
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Allocates** (using malloc) and returns a substring of the string given as argument. The substring starts at index "start" and has a maximum size of "len" | The string from which to create the substring | The starting index of the substring in the string | The maximum length of the substring | The substring. NULL if the allocation fails

## [ft_strjoin](../0/libft/ft_strjoin.c)

``` c
char *ft_strjoin (char const *s1, char const *s2)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Allocate** (with malloc) and return a new string, the result of the concatenation of "s1" and "s2" | The prefix string | The suffix string | The new string. NULL if the allocation fails

## [ft_strtrim](../0/libft/ft_strtrim.c)

``` c
char *ft_strjoin (char const *s1, char const *set)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Allocates** (using malloc) and returns a copy of the string given as argument without the characters specified in the "set" argument at the beginning and end of the string | The string to trim | The reference character set to trim | The trimmed string. NULL if the allocation fails

## [ft_split](../0/libft/ft_split.c)

``` c
char **ft_split (char const *s, char c)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Allocates** (using malloc) and returns an array of strings (terminated by a NULL pointer) obtained by splitting the string "s" using the character "c" as a delimiter. Do not include the delimiter in the resulting strings. | The string to split | The delimiter character used to separate the substrings | An array of strings resulting from the split. NULL if the assignment fails

## [ft_itoa](../0/libft/ft_itoa.c)

``` c
char   *ft_itoa (int n)`
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
**Assign** (with malloc) and return a string representing the integer received as an argument. Negative numbers must be handled | The integer to convert | The string representing the integer. NULL if the assignment fails

## [ft_strmapi](../0/libft/ft_strmapi.c)

``` c
char *ft_strmapi (char const *s, char (*f)(unsigned int, char))
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Applies** the function "f" to each character of the string passed as an argument to create a new string (with malloc) resulting from successive applications of "f" | The string to iterate over | The function to apply to each character | The string created from successive applications of "f". Returns NULL if the assignment fails
## [ft_striteri](../0/libft/ft_striteri.c)

``` c
void ft_striteri (char *s, void (*f)(unsigned int, char*))
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Applies** the `f` function to each character in the string `s`, providing its index as the first argument. The `f` function can modify characters directly in the string. It is useful for modifying characters in a string in an indexed manner, without returning a new string. | The string to apply the function to, passed as modifiable. | The function to apply to each character, receiving the character index as the first parameter and a pointer to the character in the string as the second parameter. | Does not return a value (`void` function).


## [ft_putchar_fd](../0/libft/ft_putchar_fd.c)

``` c
void ft_putchar_fd (char c, int fd)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Send** the character 'c' to the specified file descriptor using the `write` function. This is useful for writing to any output, such as the terminal (stdout), a file, or a socket, depending on the file descriptor. | The character to send | The file descriptor to write to: `0` (stdin), `1` (stdout), `2` (stderr), or any valid file descriptor | No value returned (`void`).


## [ft_putstr_fd](../0/libft/ft_putstr_fd.c)

``` c
void ft_putstr_fd (char *s, int fd)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Send** the string `s` to the specified file descriptor using the `write` function. This is useful for writing to any output, such as the terminal (stdout), a file, or a socket, depending on the file descriptor. | The string to send | The file descriptor to write to: `0` (stdin), `1` (stdout), `2` (stderr), or any valid file descriptor | No value returned (`void`).


## [ft_putendl_fd](../0/libft/ft_putendl_fd.c)

``` c
void ft_putendl_fd(char *s, int fd)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Send** the string `s` to the specified file descriptor, followed by a newline (`'\n'`), using the `write` function. This is useful for writing a string followed by a newline to any output, such as the terminal (stdout), a file, or a socket, depending on the file descriptor. | The string to send | The file descriptor to write to: `0` (stdin), `1` (stdout), `2` (stderr), or any valid file descriptor | No value returned (`void`).


## [ft_putnbr_fd](../0/libft/ft_putnbr_fd.c)

``` c
void ft_putnbr_fd(int n, int fd)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Send** the integer `n` to the specified file descriptor using the `write` function. This function converts the number to its character representation and then sends it to the file descriptor. | The integer to be sent | The file descriptor to write to: `0` (stdin), `1` (stdout), `2` (stderr), or any valid file descriptor | No value returned (`void`).

<br><br><br><br><br>

# Bonus part

## Add the declaration to your libft.h file:


``` c
typedef	struct	s_list
{
	void			*content;
	struct s_list	*next;
}					t_list;
```

Los miembros de la estructura t_list son:

• **content:** the information contained by the node.

__void *__: allows you to save any type of information.

• **next:** the address of the next node, or NULL if the next node is the last one.

In your Makefile, add a make bonus rule that incorporates the bonus functions into your
libft.a


## [ft_lstnew](../0/libft/ft_lstnew_bonus.c)

``` c
t_list *ft_lstnew(void *content)`
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
**Creates** a new node of type `t_list` using `malloc`. The member variable `content` is initialized to the contents of the `content` parameter, and the `next` variable is initialized to `NULL`. | The content to be assigned to the new node | A pointer to the newly created node. NULL if the allocation fails.


## [ft_lstadd_front](../0/libft/ft_lstadd_front_bonus.c)

``` c
void ft_lstadd_front(t_list **lst, t_list *new)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Adds** the node `new` to the beginning of the list `lst`. Updates the list pointer to point to the new node, making it the first node in the list. | The address of a pointer to the first node in the list | A pointer to the node to be added to the beginning of the list | Returns no value (`void`).


## [ft_lstsize](../0/libft/ft_lstsize_bonus.c)

``` c
int ft_lstsize(t_list *lst)`
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
**Count** the number of nodes in the linked list starting from the `lst` node. | The pointer to the first node in the list | The length of the list (number of nodes).


## [ft_lstlast](../0/libft/ft_lstlast_bonus.c)

``` c
t_list *ft_lstlast(t_list *lst)`
```

Description | Param. #1 | Return Value
:-----------: | :-----------: | :-----------:
**Returns** the last node of the linked list starting from the node `lst`. | The pointer to the first node in the list | A pointer to the last node in the list. If the list is empty, returns `NULL`.


## [ft_lstadd_back](../0/libft/ft_lstadd_back_bonus.c)

``` c
void ft_lstadd_back(t_list **lst, t_list *new)
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Adds** the node `new` to the end of the list `lst`. If the list is empty, `new` becomes the first node. | A pointer to the pointer to the first node in the list | A pointer to the node to be added to the end of the list | Returns no value (`void`).


## [ft_lstdelone](../0/libft/ft_lstdelone_bonus.c)

``` c
void ft_lstdelone(t_list *lst, void (*del)(void *))`
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Takes** an `lst` node as a parameter and frees the contents memory using the `del` function given as a parameter, in addition to freeing the node itself. The memory of `next` must not be freed. | The node to be freed | A pointer to the function used to free the contents of the node | Returns no value (`void`).


## [ft_lstclear](../0/libft/ft_lstclear_bonus.c)

``` c
void ft_lstclear(t_list **lst, void (*del)(void *))
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Removes** and frees the given `lst` node and all consecutive nodes, using the `del` function to free the contents of each node, and `free` to free the nodes themselves. At the end, the pointer to the list must be `NULL`. | The address of a pointer to the first node in the list | A pointer to the function used to remove the contents of each node | Returns no value (`void`).

## [ft_lstiter](../0/libft/ft_lstiter_bonus.c)

``` c
void ft_lstiter(t_list *lst, void (*f)(void *))
```

Description | Param. #1 | Param. #2 | Return Value
:-----------: | :-----------: | :-----------: | :-----------:
**Iterates** over the list `lst` and applies the function `f` to the contents of each node. | A pointer to the first node in the list | A pointer to the function to be applied to each node | Returns no value (`void`).

## [ft_lstmap](../0/libft/ft_lstmap_bonus.c)

``` c
t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))
```

Description | Param. #1 | Param. #2 | Param. #3 | Return Value
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Iterates** over the list `lst` and applies the function `f` to the contents of each node, creating a new list from the results. The `del` function is used to remove the contents of a node if necessary. | A pointer to the first node in the list | The address of a pointer to the function that transforms the contents of each node | A pointer to the function used to free the contents of a node, if necessary | A pointer to the newly created list. `NULL` if the memory allocation fails.
