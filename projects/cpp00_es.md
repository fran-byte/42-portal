---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 CPP00 – Introducción a C++ y Programación Orientada a Objetos

### 📌 Objetivo:

Introducir conceptos básicos de C++: **clases**, **funciones miembro**, **streams**, **const**, **static**, y listas de inicialización. Énfasis en estilos orientados a objetos siguiendo el estándar C++98.

---

## 📁 ex00 – Megaphone

### 🎯 Objetivo:

* Escribir un programa que convierta la entrada en **mayúsculas**.

### 📦 Detalles:

* Archivos: `megaphone.cpp`, `Makefile`
* Entrada: argumentos por consola
* Salida:

  * Si no hay argumentos: `* LOUD AND UNBEARABLE FEEDBACK NOISE *`
  * Si hay argumentos: imprimirlos en mayúsculas

```bash
$> ./megaphone Hello there
HELLO THERE
```

### 🧠 Conceptos útiles:

* Uso de `std::string`, `std::toupper` (cctype)
* Iteración de strings con bucles `for`
* Uso de `argc` y `argv[]`

---

## 📁 ex01 – My Awesome PhoneBook

### 🎯 Objetivo:

Crear una **agenda** interactiva con 8 contactos máximo, permitiendo:

* Añadir (`ADD`)
* Buscar (`SEARCH`)
* Salir (`EXIT`)

### 📦 Detalles:

* Archivos: `*.cpp`, `*.hpp`, `Makefile`
* Dos clases:

  * `PhoneBook`: maneja contactos (array estático de 8)
  * `Contact`: almacena info de cada contacto

### 🧠 Consideraciones:

* Si se añade el 9no contacto, reemplaza el más antiguo
* Campos: nombre, apellido, apodo, teléfono, secreto
* Los listados deben truncar cadenas >10 caracteres con `.` final

```bash
$> ./phonebook
ADD
SEARCH
EXIT
```

### 🔧 Recursos útiles para implementación:

* `std::string`, `std::getline()`
* `std::setw`, `std::right`, `std::left`, `std::cout`
* `stringstream` para formateo y truncado de cadenas
* Validación de entrada básica y bucles `while` para mantener el programa activo

### 🧩 Sugerencia de diseño:

* Clase `Contact`: setters y getters simples para cada campo
* Clase `PhoneBook`: array de 8 contactos + índice cíclico para reemplazo
* Método `displayTable()` para formato SEARCH y `displayDetails()` para mostrar un contacto en profundidad

---

## 📊 Consejos Generales

* Compilar siempre con:

```bash
c++ -Wall -Wextra -Werror -std=c++98
```

* Usa nombres significativos y formato UpperCamelCase para clases
* No pongas implementaciones en headers (salvo templates)
* Evita leaks: usa `delete` correctamente (aunque en este módulo no hay `new`/`delete`)

---

## 📚 Recursos

* [cplusplus.com](https://cplusplus.com/)
* [cppreference.com](https://en.cppreference.com/)
* `man string`, `man iomanip`, `man ctime`

---
