---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Fundamentos previos (antes de atacar pipex)

### 📌 Objetivo:

Reproducir el comportamiento de las **tuberías (`|`) y redirecciones de entrada/salida de la shell**, utilizando llamadas al sistema en C. Tu programa debe **ejecutar dos comandos en secuencia**, redirigiendo entrada y salida a archivos, y **conectándolos entre sí mediante una tubería**.

---

## 🔧 ¿Qué hace `pipex`?

Ejecuta dos comandos encadenados, conectando su entrada y salida de forma controlada:

```bash
./pipex infile cmd1 cmd2 outfile
````

Es equivalente a lo que harías en la shell:

```bash
< infile cmd1 | cmd2 > outfile
```

📌 Es decir:

* La entrada de `cmd1` proviene de un archivo.
* Su salida se conecta a la entrada de `cmd2` usando un `pipe`.
* La salida final de `cmd2` se redirige a otro archivo.

---

## 🔁 Flujo de ejecución del programa

1. Abrir `infile` y redirigirlo como `stdin` de `cmd1`.
2. Crear un `pipe` para conectar `cmd1` y `cmd2`.
3. Redirigir la salida (`stdout`) de `cmd1` al pipe.
4. Redirigir la entrada (`stdin`) de `cmd2` al pipe.
5. Abrir `outfile` y redirigir la salida de `cmd2` allí.

📌 Cada uno de estos pasos se realiza en procesos hijos creados con `fork()`.

---

## 🧠 Funciones clave del proyecto

| Función    | Descripción                                                    |
| ---------- | -------------------------------------------------------------- |
| `pipe()`   | Crea un canal de comunicación (pipe) entre procesos.           |
| `fork()`   | Crea un proceso hijo para ejecutar un comando.                 |
| `dup2()`   | Redirige `stdin` o `stdout` a un descriptor de archivo o pipe. |
| `execve()` | Ejecuta el comando especificado (reemplaza el proceso actual). |
| `open()`   | Abre archivos para lectura o escritura.                        |
| `close()`  | Cierra descriptores innecesarios.                              |
| `wait()`   | Espera a que los hijos terminen para evitar procesos zombies.  |

---

## 📦 Búsqueda del `PATH` (resolución de comandos)

Para ejecutar un comando como `"ls"` o `"grep"`, debes buscarlo en los directorios de la variable de entorno `PATH`:

### 🔍 Proceso:

1. Obtener la variable `PATH` desde `envp[]`.
2. Separar los directorios por `:`.
3. Combinar cada directorio con el nombre del comando.
4. Verificar si es ejecutable con `access(path, X_OK)`.
5. Pasar esa ruta a `execve()`.

---

## 🧪 Ejemplo de uso

```bash
./pipex input.txt "grep hello" "wc -l" output.txt
```

Equivale a:

```bash
< input.txt grep hello | wc -l > output.txt
```

✅ Flujo:

1. `input.txt` → `stdin` de `grep hello`
2. `stdout` de `grep hello` → `stdin` de `wc -l` (mediante pipe)
3. `stdout` de `wc -l` → `output.txt`

---

## ⚙️ Diagrama de flujo

![Diagrama pipex](../../img/milestone_2/pipex_flujo.png)

---

## 📉 Problemas comunes

1. ❌ **Descriptores mal cerrados**: pueden causar deadlocks o fugas.
2. 🔐 **Permisos de archivos**: asegúrate de tener acceso de lectura/escritura.
3. 🚫 **Errores en llamadas del sistema**: siempre usa `perror()` o `strerror(errno)` para depurar.

---

## 🛠️ Funciones autorizadas

Puedes usar:

* `open`, `close`, `read`, `write`, `malloc`, `free`, `perror`, `strerror`
* `access`, `dup`, `dup2`, `execve`, `exit`, `fork`, `pipe`, `unlink`, `wait`, `waitpid`
* Tu propia implementación de `ft_printf` si lo necesitas.

---

## 🧱 Estructura mínima del proyecto

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

## 📚 Recursos útiles

* [`man 2 pipe`](https://man7.org/linux/man-pages/man2/pipe.2.html)
* [`man 2 execve`](https://man7.org/linux/man-pages/man2/execve.2.html)
* [`man 3 access`](https://man7.org/linux/man-pages/man3/access.3p.html)
* [Artículo: cómo funcionan las pipes en C (español)](https://www.cs.buap.mx/~hilario_sm/slide/SO-1/Pipe.pdf)

---

## 🧠 Consejos prácticos

* ✨ Empieza resolviendo un comando sencillo antes de implementar los `fork()`.
* 💡 Implementa la búsqueda de comandos (`PATH`) como una función separada.
* 🧪 Prueba con archivos reales y errores controlados (ficheros inexistentes, sin permisos...).
* 🧼 Limpia bien los `malloc` y los `pipes`, usa `valgrind`.
* 📦 No olvides verificar argumentos: número correcto, existencia de archivos, etc.

---
