---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Fundamentos previos (antes de atacar ft_printf)

### 📌 Objetivo:

### 🧠 Conceptos clave antes de comenzar

#### ✅ `write(int fd, const void *buf, size_t count)`

Es la función básica que usarás para imprimir:

```c
write(1, &c, 1);  // imprime un solo carácter
```

#### ✅ `va_list` (variadic functions)

Para manejar argumentos variables (`...`) necesitamos usar macros del archivo <stdarg.h> :

```c
#include <stdarg.h>

va_list args;
va_start(args, format);
... // va_arg(args, type)
va_end(args);
```
va_list: Declara una variable que mantendrá la información sobre los argumentos adicionales.

va_start: Inicializa la variable del tipo va_list con los parámetros variables.

va_arg: Se utiliza para extraer cada argumento.

va_end: Limpia la lista de argumentos cuando se han procesado todos.

---

### 💡 **TIP — Cómo funcionan las funciones variádicas**

Las funciones con `...` (como `ft_printf`) **no saben cuántos argumentos adicionales reciben ni qué tipo son**. Tú debes procesarlos uno por uno usando macros de `stdarg.h`:

```c
va_list args;
va_start(args, format);      // Inicia la lista de argumentos
int n = va_arg(args, int);   // Extrae el siguiente argumento como int
va_end(args);                // Finaliza el uso de la lista
```

> ⚠️ ¡El orden de extracción debe coincidir exactamente con los tipos esperados en el `format`! Si lees un `char *` cuando hay un `int`, tendrás comportamiento indefinido.

---

### 🖨️ ¿Qué es `ft_printf`?

Es una reimplementación de la función estándar `printf` de C, que permite mostrar información formateada en la salida estándar.

Tu función debe comportarse como `printf`, pero solo con un **subconjunto de formatos** definidos por el proyecto (como `%c`, `%s`, `%d`, `%x`, etc.).

---

### 🔧 ¿Cómo se usa?

```c
ft_printf("Character: %c\n", 'A');
ft_printf("String: %s\n", "Hello");
ft_printf("Number: %d\n", 42);
ft_printf("Hex: %x\n", 255);
````

> ✅ Debe devolver el **número de caracteres impresos**, como `printf`.

---

### 🧠 Conceptos clave antes de comenzar

#### ✅ `write(int fd, const void *buf, size_t count)`

Es la función básica que usarás para imprimir:

```c
write(1, &c, 1);  // imprime un solo carácter
```

#### ✅ `va_list` (variadic functions)

Para manejar argumentos variables (`...`) necesitas:

```c
#include <stdarg.h>

va_list args;
va_start(args, format);
... // va_arg(args, type)
va_end(args);
```

---

### 📦 ¿Qué debes implementar?

#### 🧾 Prototipo obligatorio:

```c
int ft_printf(const char *format, ...);
```

#### 🎯 Formatos requeridos por el subject:

| Especificador | Significado               |
| ------------- | ------------------------- |
| `%c`          | Character                 |
| `%s`          | String                    |
| `%p`          | Pointer address           |
| `%d` / `%i`   | Signed integer            |
| `%u`          | Unsigned integer          |
| `%x` / `%X`   | Hexadecimal (lower/upper) |
| `%%`          | Print literal `%`         |

---

### 🧱 Estructura mínima del proyecto

```
ft_printf/
├── ft_printf.c
├── ft_printf.h
├── ft_utils.c
├── main.c (para pruebas)
```

---

### ⚙️ Compilación recomendada

```bash
cc -Wall -Wextra -Werror ft_printf.c ft_utils.c main.c
```

> ❗ No uses funciones prohibidas como `printf`, `itoa`, `sprintf`, etc.

---

### 🧩 Tips técnicos para implementar `ft_printf`

* **Divide y vencerás**: crea una función por tipo de formato.
* Usa `va_arg` para acceder a los argumentos dinámicos.
* Crea tus propias versiones de:

  * `ft_strlen`
  * `ft_putnbr`
  * `ft_putstr`
  * `ft_itoa_base` para hexadecimales
* Usa contadores para llevar la cuenta de caracteres impresos.
* Gestiona punteros (`%p`) convirtiendo a hexadecimal y anteponiendo `0x`.

---

### 📚 Recursos útiles

* `man 3 printf`
* `man 2 write`
* `man stdarg`
* [printf specification on cppreference.com](https://en.cppreference.com/w/c/io/fprintf)

---

### 🧠 Consejos prácticos

* Empieza implementando `%c`, `%s` y `%%` para entender el flujo.
* Asegúrate de contar bien los caracteres que imprimes (¡es lo que devuelve tu función!).
* Usa `valgrind` para detectar fugas, sobre todo con `%p` y strings.
* Testea cada tipo de formato con casos borde (ej. NULL strings, valores negativos, hexadecimales grandes).
* Haz una tabla o switch para despachar cada tipo de argumento.

---
