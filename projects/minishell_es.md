---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Fundamentos Previos (Antes de Empezar Minishell)

### 📌 Objetivo:

El proyecto **Minishell** tiene como objetivo implementar una mini interfaz de línea de comandos (shell) capaz de ejecutar comandos como lo hace una shell de Unix real, con soporte para pipes, redirecciones, variables de entorno y manejo de señales. Desarrollarás una comprensión profunda del comportamiento de las shells y las llamadas al sistema en Linux.

---

## 🔹 2. Comportamiento Esperado

### 🚀 Tu minishell debe ser capaz de:

* Mostrar un prompt y esperar comandos.
* Ejecutar comandos con argumentos.
* Soportar redirecciones: `>`, `>>`, `<`, `<<`.
* Ejecutar comandos encadenados con pipes: `ls | grep txt`.
* Manejar comillas simples y dobles correctamente.
* Gestionar variables de entorno: `$USER`, `$PATH`, etc.
* Implementar comandos internos como `cd`, `echo`, `pwd`, `export`, `unset`, `env`, `exit`.
* Manejar el `Ctrl+C`, `Ctrl+D` y `Ctrl+́` (señales de interrupción).

---

## 🪧 3. Funciones y Conceptos Clave

| Función                  | Uso principal                                  |
| ------------------------ | ---------------------------------------------- |
| `fork()`                 | Crear un proceso hijo                          |
| `execve()`               | Reemplazar el proceso con uno nuevo            |
| `pipe()`                 | Crear comunicación entre procesos              |
| `dup2()`                 | Redirigir descriptores de archivo              |
| `waitpid()`              | Esperar la finalización de un hijo             |
| `read()`/`write()`       | Lectura y escritura en ficheros o descriptores |
| `open()`                 | Abrir archivos con flags de modo               |
| `close()`                | Cerrar descriptores                            |
| `signal()`/`sigaction()` | Manejar señales del sistema                    |
| `getenv()`               | Obtener variables del entorno                  |
| `setenv()`/`unsetenv()`  | Establecer/eliminar variables del entorno      |

---

## 📃 4. Estructura del Proyecto

```
minishell/
├── minishell.c         // Main loop y parsing
├── parser.c            // Parseo de comandos, tokens, quotes
├── executor.c          // Ejecución de comandos y redirecciones
├── builtin.c           // Implementación de comandos internos
├── signals.c           // Gestión de señales
├── env.c               // Gestión de variables de entorno
├── utils/              // Utilidades comunes
├── includes/           // Headers
```

---

## 📈 5. Gestión de Señales

Tu minishell debe:

* Ignorar `Ctrl+\` (`SIGQUIT`) mientras no se ejecuta un comando.
* Manejar `Ctrl+C` (`SIGINT`) para cancelar el comando actual y mostrar un nuevo prompt.
* Gestionar correctamente `Ctrl+D` (EOF): salir si el prompt está vacío.

---

## 🔍 6. Redirecciones

| Redirección | Significado                                       |
| ----------- | ------------------------------------------------- |
| `>`         | Redirige stdout a un archivo (sobrescribe)        |
| `>>`        | Redirige stdout a un archivo (añade al final)     |
| `<`         | Redirige stdin desde un archivo                   |
| `<<`        | Here-document: stdin desde una entrada delimitada |

---

## 🤖 7. Variables de Entorno

### Implementar soporte para:

* Expansión de variables con `$NOMBRE`.
* Exportación de nuevas variables con `export`.
* Eliminación con `unset`.
* Listado con `env`.

---

## 🚛 8. Ejemplo de Ejecución

```bash
$ echo "Hola mundo"
Hola mundo

$ export USERNAME=fran
$ echo $USERNAME
fran

$ cat << EOF
> línea 1
> línea 2
> EOF
línea 1
línea 2

$ ls | grep .c > archivos.txt
```

---

## 🚧 9. Comandos Internos (built-ins)

* `cd [path]`
* `pwd`
* `echo [args]`
* `export VAR=valor`
* `unset VAR`
* `env`
* `exit`

---

## 📊 10. Consejos Prácticos

* Usa estructuras para representar comandos, tokens, redirecciones.
* Implementa parsing robusto (quotes, escapes, pipes, múltiples redirs).
* Desarrolla primero comandos simples y luego agrega funcionalidades.
* Testea errores de memoria con Valgrind:

```bash
valgrind --leak-check=full ./minishell
```

---

## 📅 11. Recursos Útiles

* `man 3 getenv`, `man 2 execve`, `man 2 pipe`, `man 2 dup2`
* [GNU Bash Manual](https://www.gnu.org/software/bash/manual/bash.html)
* [Shell Command Language (POSIX)](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html)

---
