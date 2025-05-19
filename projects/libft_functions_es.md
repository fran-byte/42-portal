---
layout: default
title: "fran-byte 42 Madrid"
---

# Parte 1 - Funciones de libc


## [ft_isalpha](../0/libft/ft_isalpha.c)

``` c
int ft_isalpha (int c)
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
Verifica si es un carácter **alfabético**.) | El carácter a probar | 0 si el carácter es falso y 1 si el carácter es verdadero

## [ft_isdigit](../0/libft/ft_isdigit.c)

``` c
int ft_isdigit (int c)
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
Verifica si es un **dígito** (0 a 9) | El carácter a probar | 0 si el carácter es falso y 1 si el carácter es verdadero

## [ft_isalnum](../0/libft/ft_isalnum.c)

``` c
int ft_isalnum (int c)
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
Verifica si es un carácter **alfanumérico** | El carácter a probar | 0 si el carácter es falso y 1 si el carácter es verdadero

## [ft_isascii](../0/libft/ft_isascii.c)

``` c
int ft_isascii (int c)
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
Verifica si es un carácter **ASCII**, que es cualquier carácter entre 0 y octal 0177 inclusive | El carácter a probar | 0 si el carácter es falso y 1 si el carácter es verdadero

## [ft_isprint](../0/libft/ft_isprint.c)

``` c
int ft_isprint (int c)
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
Verifica si es un carácter **imprimible**, incluido el espacio | El carácter a probar | 0 si el carácter es falso y 1 si el carácter es verdadero

## [ft_strlen](../0/libft/ft_strlen.c)
``` c
size_t ft_strlen (const char *s)
```

Descripción | Param. #1 | Valores de Retorno
:-----------: | :-----------: | :-----------:
Calcula la **longitud** de la cadena apuntada por "s", excluyendo el byte nulo de terminación ('\0') | La cadena a calcular | Número de caracteres en la cadena apuntada por "s"

## [ft_memset](../0/libft/ft_memset.c)

``` c
void *ft_memset (void *s, int c, size_t len)
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Rellena** con "len" bytes de "c" la memoria de "s" | La cadena sobre la que operar | Valor c (convertido a unsigned char) | El número de bytes | Un puntero al área de memoria s

## [ft_bzero](../0/libft/ft_bzero.c)

``` c
void *ft_bzero (void *s,  size_t n)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Borra** los datos en los "n" bytes de la memoria comenzando en la ubicación señalada por "s", escribiendo ceros | La cadena sobre la que operar | El número de bytes | Ninguno

## [ft_memcpy](../0/libft/ft_memcpy.c)

``` c
void *ft_memcpy (void *dst, const void *src, size_t n)
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Copia** "n" bytes del área de memoria "src" a la memoria de "dst". Las áreas de memoria no deben solaparse (Si el tamaño de dst es menor que n) **puede sobrescribir memoria adyacente**. Usa [ft_memmove](#ft_memmove) si las áreas de memoria se solapan. | Área de memoria dst | Área de memoria src | El número de bytes | Un puntero al área de memoria dst

## [ft_memmove](../0/libft/ft_memmove.c)

``` c
void *ft_memmove (void *dst, const void *src, size_t len)
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Copia** "len" bytes de la memoria de "src" a "dst". Las memorias pueden solaparse. Primero, los bytes en "src" se copian en un arreglo temporal y luego a "dst". (Si el tamaño de dst es menor que n) **puede sobrescribir memoria adyacente** | Área de memoria dst | Área de memoria src | El número de bytes | Un puntero al área de memoria dst

## [ft_strlcpy](../0/libft/ft_strlcpy.c)

``` c
size_t ft_strlcpy (char *dst, const char *src, size_t dstsize)
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Copia** hasta "dstsize - 1" caracteres de la cadena terminada en NUL "src" a "dst", terminando en NUL el resultado | Arreglo de destino | Cadena a copiar | Número de caracteres a copiar de "src" | Longitud total de la cadena creada (longitud de "src")

## [ft_strlcat](../0/libft/ft_strlcat.c)

``` c
size_t ft_strlcat (char *dst, const char *src, size_t size)
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Concatena** la cadena "src" al final de "dst". Concatenará como máximo "size - strlen(dst) - 1" bytes, terminando en NUL el resultado | Arreglo de destino | Cadena a agregar a "dst" | Número máximo de caracteres a agregar | La longitud inicial de "dst" más la longitud de "src"

## [ft_toupper](../0/libft/ft_toupper.c)

``` c
int ft_toupper (int c)
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
Si el carácter pasado como argumento es una letra minúscula, se convierte a **mayúscula** | El carácter a convertir | Si "c" es una letra minúscula, devuelve su equivalente en mayúscula. De lo contrario, devuelve "c"

## [ft_tolower](../0/libft/ft_tolower.c)

``` c
int ft_tolower (int c)
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
Si el carácter pasado como argumento es una letra mayúscula, se convierte a **minúscula** | El carácter a convertir | Si "c" es una letra mayúscula, devuelve su equivalente en minúscula. De lo contrario, devuelve "c"

## [ft_strchr](../0/libft/ft_strchr.c)

``` c
char *ft_strchr (const char *s, int c)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
Localiza la **primera** ocurrencia de "c" en la cadena apuntada por "s". El carácter nulo de terminación se considera parte de la cadena, por lo tanto, si "c" es '\0', localiza el '\0' final | Puntero a la cadena | Carácter a localizar | Un puntero a la primera ocurrencia del carácter "c" en la cadena o NULL si no se encuentra el carácter

## [ft_strrchr](../0/libft/ft_strrchr.c)

``` c
char *ft_strrchr (const char *s, int c)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
Localiza la **última** ocurrencia de "c" en la cadena apuntada por "s". El carácter nulo de terminación se considera parte de la cadena, por lo tanto, si "c" es '\0', localiza el '\0' final | Puntero a la cadena | Carácter a localizar | Un puntero a la última ocurrencia del carácter "c" en la cadena o NULL si no se encuentra el carácter

## [ft_strncmp](../0/libft/ft_strncmp.c)

``` c
int ft_strncmp (const char *s1, const char *s2, size_t n)
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Compara** los primeros "n" bytes de las cadenas "s1" y "s2".| Cadena 1 para comparar | Cadena 2 para comparar | El número de bytes a comparar | Un entero negativo, cero o positivo, dependiendo de si "s1" es menor, igual o mayor que "s2".

## [ft_memchr](../0/libft/ft_memchr.c)

``` c
void *ft_memchr (const void *s, int c, size_t n)
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Escanea** los primeros "n" bytes de "s" en busca de la primera instancia de "c" | Área de memoria s | Un carácter a buscar | El número de bytes | Un puntero al byte coincidente o NULL si el carácter no aparece en el área de memoria dada

## [ft_memcmp](../0/libft/ft_memcmp.c)

``` c
void *ft_memcmp (void *dst, const void *src, size_t n)
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Compara** la cadena de bytes "s1" con la cadena de bytes "s2" | Área de memoria s1 | Área de memoria s2 | El número de bytes | < 0 si s1 es menor que s2, > 0 si s1 es mayor que s2, = 0 si s1 es igual a s2

## [ft_strnstr](../0/libft/ft_strnstr.c)

``` c
char *ft_strnstr (const char *haystack, const char *needle, size_t len)`
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Localiza** una subcadena, donde no se buscan más de "len" caracteres. Encuentra la primera ocurrencia de la subcadena "needle" en la cadena "haystack". Los bytes nulos de terminación ('\0') no se comparan | Cadena donde buscar | La subcadena a buscar en "haystack" | El número máximo de caracteres a buscar | Un puntero al primer carácter de la primera ocurrencia de "needle". NULL si la subcadena no se encuentra. Si "needle" es una cadena vacía, se devuelve "haystack"

## [ft_atoi](../0/libft/ft_atoi.c)

``` c
int ft_atoi (const char *str)
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
**Convierte** una cadena en un entero | La cadena a convertir en entero | El valor convertido


## [ft_calloc](../0/libft/ft_calloc.c)

``` c
void *ft_calloc (size_t count, size_t size)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Asigna** suficiente espacio para "count" objetos, cada uno de "size" bytes de memoria, y devuelve un puntero a la memoria asignada. La memoria asignada se llena con bytes de valor cero | Número de elementos a asignar | Tamaño de los elementos | Un puntero a la memoria asignada, o NULL si la solicitud falla


## [ft_strdup](../0/libft/ft_strdup.c)

``` c
char *ft_strdup (const char *s)`
```

Descripción | Param. #1 | Valores de Retorno
:-----------: | :-----------: | :-----------:
**Duplica** la cadena "s". La memoria para la nueva cadena se obtiene con malloc y puede ser liberada con free | La cadena a duplicar | Un puntero a la cadena duplicada. NULL si no había suficiente memoria disponible

<br><br><br><br><br>

# Parte 2 - Funciones adicionales

## [ft_substr](../0/libft/ft_substr.c)

``` c
char *ft_substr (char const *s, unsigned int start, size_t len)
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Asigna** (con malloc) y devuelve una subcadena de la cadena dada como argumento. La subcadena comienza en el índice "start" y tiene un tamaño máximo de "len" | La cadena de la cual crear la subcadena | El índice de inicio de la subcadena en la cadena | La longitud máxima de la subcadena | La subcadena. NULL si la asignación falla

## [ft_strjoin](../0/libft/ft_strjoin.c)

``` c
char *ft_strjoin (char const *s1, char const *s2)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Asigna** (con malloc) y devuelve una nueva cadena, resultado de la concatenación de "s1" y "s2" | La cadena prefijo | La cadena sufijo | La nueva cadena. NULL si la asignación falla

## [ft_strtrim](../0/libft/ft_strtrim.c)

``` c
char *ft_strjoin (char const *s1, char const *set)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Asigna** (con malloc) y devuelve una copia de la cadena dada como argumento sin los caracteres especificados en el argumento "set" al principio y al final de la cadena | La cadena a recortar | El conjunto de caracteres de referencia para recortar | La cadena recortada. NULL si la asignación falla

## [ft_split](../0/libft/ft_split.c)

``` c
char **ft_split (char const *s, char c)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Asigna** (con malloc) y devuelve un array de cadenas (terminado por un puntero NULL) obtenidas al dividir la cadena "s" usando el carácter "c" como delimitador. No incluye el delimitador en las cadenas resultantes. | La cadena a dividir | El carácter delimitador usado para separar las subcadenas | Un array de cadenas resultante de la división. NULL si la asignación falla

## [ft_itoa](../0/libft/ft_itoa.c)

``` c
char   *ft_itoa (int n)`
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
**Asigna** (con malloc) y devuelve una cadena que representa el entero recibido como argumento. Los números negativos deben ser manejados | El entero a convertir | La cadena que representa el entero. NULL si la asignación falla

## [ft_strmapi](../0/libft/ft_strmapi.c)

``` c
char *ft_strmapi (char const *s, char (*f)(unsigned int, char))
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Aplica** la función "f" a cada carácter de la cadena pasada como argumento para crear una nueva cadena (con malloc) resultante de las aplicaciones sucesivas de "f" | La cadena sobre la que iterar | La función a aplicar a cada carácter | La cadena creada a partir de las aplicaciones sucesivas de "f". Devuelve NULL si la asignación falla

## [ft_striteri](../0/libft/ft_striteri.c)

``` c
void ft_striteri (char *s, void (*f)(unsigned int, char*))
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Aplica** la función "f" a cada carácter de la cadena "s", proporcionando su índice como primer argumento. La función `f` puede modificar los caracteres directamente en la cadena. Es útil para modificar los caracteres de una cadena de manera indexada, sin necesidad de devolver una nueva cadena. | La cadena sobre la que se aplicará la función, pasada como modificable. | La función que se aplicará a cada carácter, recibe el índice del carácter como primer parámetro y un puntero al carácter en la cadena como segundo parámetro. | No devuelve ningún valor (función `void`).


## [ft_putchar_fd](../0/libft/ft_putchar_fd.c)

``` c
void ft_putchar_fd (char c, int fd)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Envía** el carácter 'c' al file descriptor especificado utilizando la función `write`. Es útil para escribir en cualquier salida, como el terminal (stdout), un archivo o un socket, dependiendo del file descriptor. | El carácter que se va a enviar | El file descriptor sobre el cual escribir: `0` (stdin), `1` (stdout), `2` (stderr) o cualquier descriptor de archivo válido | No devuelve ningún valor (`void`).


## [ft_putstr_fd](../0/libft/ft_putstr_fd.c)

``` c
void ft_putstr_fd (char *s, int fd)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Envía** la cadena de caracteres `s` al file descriptor especificado utilizando la función `write`. Es útil para escribir en cualquier salida, como el terminal (stdout), un archivo o un socket, dependiendo del file descriptor. | La cadena de caracteres que se va a enviar | El file descriptor sobre el cual escribir: `0` (stdin), `1` (stdout), `2` (stderr) o cualquier descriptor de archivo válido | No devuelve ningún valor (`void`).


## [ft_putendl_fd](../0/libft/ft_putendl_fd.c)

``` c
void ft_putendl_fd(char *s, int fd)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Envía** la cadena de caracteres `s` al file descriptor especificado, seguido de un salto de línea (`'\n'`), utilizando la función `write`. Es útil para escribir una cadena seguida de un salto de línea en cualquier salida, como la terminal (stdout), un archivo o un socket, dependiendo del file descriptor. | La cadena de caracteres que se va a enviar | El file descriptor sobre el cual escribir: `0` (stdin), `1` (stdout), `2` (stderr) o cualquier descriptor de archivo válido | No devuelve ningún valor (`void`).


## [ft_putnbr_fd](../0/libft/ft_putnbr_fd.c)

``` c
void ft_putnbr_fd(int n, int fd)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Envía** el número entero `n` al file descriptor especificado utilizando la función `write`. Esta función convierte el número a su representación en caracteres y luego lo envía al file descriptor. | El número entero que se va a enviar | El file descriptor sobre el cual escribir: `0` (stdin), `1` (stdout), `2` (stderr) o cualquier descriptor de archivo válido | No devuelve ningún valor (`void`).

<br><br><br><br><br>

# Parte bonus

## Añade la declaración a tu archivo libft.h :


``` c
typedef	struct	s_list
{
	void			*content;
	struct s_list	*next;
}					t_list;
```

Los miembros de la estructura t_list son:

• **content:** la información contenida por el nodo.

 __void  *__: permite guardar cualquier tipo de información.

• **next:** la dirección del siguiente nodo, o NULL si el siguiente nodo es el último.

En tu Makefile, añade una regla make bonus que incorpore las funciones bonus a tu
libft.a


## [ft_lstnew](../0/libft/ft_lstnew_bonus.c)

``` c
t_list *ft_lstnew(void *content)`
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
**Crea** un nuevo nodo de tipo `t_list` utilizando `malloc`. La variable miembro `content` se inicializa con el contenido del parámetro `content`, y la variable `next` se inicializa en `NULL`. | El contenido que se asignará al nuevo nodo | Un puntero al nuevo nodo creado. NULL si la asignación falla.


## [ft_lstadd_front](../0/libft/ft_lstadd_front_bonus.c)

``` c
void ft_lstadd_front(t_list **lst, t_list *new)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Añade** el nodo `new` al principio de la lista `lst`. Actualiza el puntero de la lista para que apunte al nuevo nodo, convirtiéndolo en el primer nodo de la lista. | La dirección de un puntero al primer nodo de la lista | Un puntero al nodo que se añadirá al principio de la lista | No devuelve ningún valor (`void`).


## [ft_lstsize](../0/libft/ft_lstsize_bonus.c)

``` c
int ft_lstsize(t_list *lst)`
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
**Cuenta** el número de nodos en la lista enlazada comenzando desde el nodo `lst`. | El puntero al primer nodo de la lista | La longitud de la lista (número de nodos).


## [ft_lstlast](../0/libft/ft_lstlast_bonus.c)

``` c
t_list *ft_lstlast(t_list *lst)`
```

Descripción | Param. #1 | Valor de Retorno
:-----------: | :-----------: | :-----------:
**Devuelve** el último nodo de la lista enlazada comenzando desde el nodo `lst`. | El puntero al primer nodo de la lista | Un puntero al último nodo de la lista. Si la lista está vacía, devuelve `NULL`.


## [ft_lstadd_back](../0/libft/ft_lstadd_back_bonus.c)

``` c
void ft_lstadd_back(t_list **lst, t_list *new)
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Añade** el nodo `new` al final de la lista `lst`. Si la lista está vacía, `new` se convierte en el primer nodo. | Un puntero al puntero que apunta al primer nodo de la lista | Un puntero al nodo que se añadirá al final de la lista | No devuelve ningún valor (`void`).


## [ft_lstdelone](../0/libft/ft_lstdelone_bonus.c)

``` c
void ft_lstdelone(t_list *lst, void (*del)(void *))`
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Toma** como parámetro un nodo `lst` y libera la memoria del contenido utilizando la función `del` dada como parámetro, además de liberar el nodo en sí. La memoria de `next` no debe liberarse. | El nodo que se va a liberar | Un puntero a la función utilizada para liberar el contenido del nodo | No devuelve ningún valor (`void`).


## [ft_lstclear](../0/libft/ft_lstclear_bonus.c)

``` c
void ft_lstclear(t_list **lst, void (*del)(void *))
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Elimina** y libera el nodo `lst` dado y todos los nodos consecutivos, utilizando la función `del` para liberar el contenido de cada nodo, y `free` para liberar los nodos en sí. Al final, el puntero a la lista debe ser `NULL`. | La dirección de un puntero al primer nodo de la lista | Un puntero a la función utilizada para eliminar el contenido de cada nodo | No devuelve ningún valor (`void`).


## [ft_lstiter](../0/libft/ft_lstiter_bonus.c)

``` c
void ft_lstiter(t_list *lst, void (*f)(void *))
```

Descripción | Param. #1 | Param. #2 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------:
**Itera** sobre la lista `lst` y aplica la función `f` al contenido de cada nodo. | Un puntero al primer nodo de la lista | Un puntero a la función que se aplicará a cada nodo | No devuelve ningún valor (`void`).

## [ft_lstmap](../0/libft/ft_lstmap_bonus.c)

``` c
t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))
```

Descripción | Param. #1 | Param. #2 | Param. #3 | Valor de Retorno
:-----------: | :-----------: | :-----------: | :-----------: | :-----------:
**Itera** sobre la lista `lst` y aplica la función `f` al contenido de cada nodo, creando una nueva lista con los resultados. La función `del` se utiliza para eliminar el contenido de un nodo si es necesario. | Un puntero al primer nodo de la lista | La dirección de un puntero a la función que transforma el contenido de cada nodo | Un puntero a la función que se utiliza para liberar el contenido de un nodo, si es necesario | Un puntero a la nueva lista creada. `NULL` si falla la reserva de memoria.
