---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 CPP00 – Introducción a C++ y Programación Orientada a Objetos

### 📌 Objetivo:

Introducir conceptos básicos de C++: **clases**, **funciones miembro**, **streams**, **const**, **static**, y listas de inicialización. Énfasis en estilos orientados a objetos siguiendo el estándar C++98.


## 🔹 ¿Qué es una clase?

Una **clase** en C++ es una **plantilla** para crear objetos. Define:

* **Atributos** (también llamados campos o miembros): representan el estado del objeto.
* **Métodos** (también llamados funciones miembro): representan el comportamiento del objeto.

---

## 🔸 Atributos (Variables miembro)

Los **atributos** son variables declaradas dentro de la clase. Pueden tener distintos niveles de acceso:

```cpp
class Animal {
private:
    std::string species;
    int age;
};
```

* Por convención, los atributos se definen como `private` para protegerlos del acceso directo desde fuera.
* Cada **instancia (objeto)** de la clase tiene su **propia copia** de estos atributos.

---

## 🔸 Métodos (Funciones miembro)

Los métodos permiten que el objeto **haga algo** o que otro código **interactúe con él**.

```cpp
class Animal {
public:
    void makeSound();
    void sleep();
};
```

Estos métodos serían llamados desde el exterior así:

```cpp
Animal dog;
dog.makeSound();
```

---

## 🔸 Constructores

Un **constructor** es una función especial que se ejecuta automáticamente cuando se crea un objeto.

```cpp
class Animal {
public:
    Animal(); // Constructor por defecto
};
```

También se puede sobrecargar:

```cpp
class Animal {
public:
    Animal(std::string type, int years);
};
```

El objetivo del constructor es **inicializar** el objeto con valores válidos desde el principio.

---

## 🔸 Destructores

Un **destructor** se ejecuta automáticamente cuando un objeto **sale de ámbito** o se **elimina**. Su función es **liberar recursos**, aunque para objetos sencillos puede estar vacío.

```cpp
class Animal {
public:
    ~Animal(); // Destructor
};
```

---

## 🔸 Setters y Getters

Para acceder de forma segura a atributos `private`, usamos **métodos públicos** llamados `setters` y `getters`.

### ✅ Setter

Un método que **asigna un valor** a un atributo:

```cpp
void setSpecies(std::string newSpecies) {
    species = newSpecies;
}
```

### ✅ Getter

Un método que **devuelve el valor** de un atributo:

```cpp
std::string getSpecies() const {
    return species;
}
```

> El modificador `const` significa que el método **no cambia** el estado del objeto.

---

## 🧩 Ejemplo completo:

```cpp
class Animal {
private:
    std::string species;
    int age;

public:
    // Constructor
    Animal(std::string sp, int ag) : species(sp), age(ag) {}

    // Destructor
    ~Animal() {}

    // Setter
    void setAge(int ag) {
        age = ag;
    }

    // Getter
    int getAge() const {
        return age;
    }

    void speak() const {
        std::cout << "I am a " << species << " and I am " << age << " years old." << std::endl;
    }
};
```

Y su uso:

```cpp
Animal cat("Feline", 3);
cat.speak();
cat.setAge(4);
std::cout << "Updated age: " << cat.getAge() << std::endl;
```

---

## 📌 Conclusión

| Concepto    | Para qué sirve                                       |
| ----------- | ---------------------------------------------------- |
| Clase       | Define un nuevo tipo de datos personalizado          |
| Atributo    | Estado interno de un objeto                          |
| Método      | Funciones que describen el comportamiento del objeto |
| Constructor | Inicializa el objeto cuando se crea                  |
| Destructor  | Limpia recursos al destruir el objeto                |
| Setter      | Método para modificar un atributo privado            |
| Getter      | Método para leer un atributo privado                 |

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
