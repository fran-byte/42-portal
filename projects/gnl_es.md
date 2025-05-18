---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Fundamentos previos (antes de atacar get_next_line)

### 📌 Objetivo:

Entender cómo funciona la **lectura de archivos en C** usando `read`, manejo de buffers, concatenación dinámica de strings, y control de memoria con `malloc` y `free`, para construir una función robusta capaz de **leer línea por línea** desde un descriptor de archivo.

---

### 📁 ¿Qué es `get_next_line`?

Es una función que lee de un file descriptor línea a línea y devuelve cada línea terminada en `\n`. Tienes que implementarla sin utilizar funciones de la libc que no estén permitidas (como `strdup`, `strjoin`, etc.).

---

### 🔧 ¿Cómo se usa?

```c
char *line;

line = get_next_line(fd);
while (line != NULL)
{
    printf("%s", line);
    free(line);
    line = get_next_line(fd);
}
````

---

### 🧠 Conceptos clave antes de comenzar

#### ✅ File descriptor (`fd`)

Un **file descriptor** es un entero que representa un archivo abierto. Por ejemplo:

* `0`: stdin
* `1`: stdout
* `2`: stderr
* `fd = open("archivo.txt", O_RDONLY);`

---

#### ✅ La función `read`

`read(fd, buffer, BUFFER_SIZE)` lee hasta `BUFFER_SIZE` bytes desde el `fd` hacia `buffer`. Devuelve:

* El número de bytes leídos
* `0` si se llega al final del archivo (EOF)
* `-1` si hay error

---

### 📦 ¿Qué debes implementar?

#### 🧾 Prototipo obligatorio:

```c
char *get_next_line(int fd);
```

Además, puedes (y debes) crear funciones auxiliares en archivos separados como:

* `ft_strjoin`
* `ft_strchr`
* `ft_strlen`
* `ft_strdup`
* `ft_substr`

---

### 🧱 Estructura mínima del proyecto

```
get_next_line/
├── get_next_line.c
├── get_next_line.h
├── get_next_line_utils.c
├── main.c (para pruebas)
```


---

### ⚙️ BUFFER\_SIZE

Debes compilar tu proyecto permitiendo que el evaluador lo defina:

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 main.c get_next_line.c get_next_line_utils.c
```

> ✅ Usa `#ifndef BUFFER_SIZE` en tu `.h` para definir un valor por defecto si no se da en compilación.

---

### 🧩 Tips técnicos para implementar `get_next_line`

* Usar un **buffer estático** o `static char *resto` para guardar lo que queda entre llamadas.
* Concatenar lo que vas leyendo hasta encontrar un `\n`.
* Cuando encuentres una línea completa, **separa lo leído de lo pendiente**.
* Al final de archivo, devuelve lo que quede en el buffer.

---

### 📚 Recursos útiles

* `man 2 read`
* `man open`, `man close`
* `valgrind` para detectar leaks
* `strchr`, `strjoin`, `strdup`, `strlen`, `substr` — si no puedes usarlas, **reimplémentalas tú mismo**.

---

### 🧠 Consejos prácticos

* Comienza implementando una versión sin `static`, para entender la lógica.
* Después, agrega el manejo de buffers estáticos para varias llamadas.
* Prueba con archivos grandes y líneas sin salto final.
* Usa `valgrind` para asegurarte de no tener fugas de memoria.
* Haz una función por responsabilidad: una para buscar el salto, otra para cortar strings, otra para limpiar memoria.

---
