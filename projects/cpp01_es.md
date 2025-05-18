---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 CPP01 – Pilares del Estilo Orientado a Objetos en C++

### 📌 Objetivo:

Consolidar el uso de clases y funciones miembro, introducir **referencias**, **const correctness**, la **sobrecarga de operadores**, y la **gestión de memoria dinámica**. Este módulo te ayudará a entender mejor la lógica y la sintaxis orientada a objetos en C++98.

---

## 📁 ex00 – Referencias y Asignación por Referencia

### 🎯 Objetivo:

Familiarizarse con el uso de **referencias** en C++, la diferencia con punteros, y cómo se usan como parámetros.

### 🧠 Teoría clave:

* Una **referencia** es un alias para otra variable.
* A diferencia de los punteros, **una referencia siempre debe estar inicializada** y no puede cambiar de dirección.

```cpp
void changeValue(int &ref) {
    ref = 42;
}
```

* Las referencias son ideales cuando quieres modificar el valor original sin copiarlo, por ejemplo, en funciones de utilidad.

---

## 📁 ex01 – Const Correctness y Uso de Clases

### 🎯 Objetivo:

* Introducir funciones `const`, constructores, destructores y funciones miembro.
* Consolidar el uso de clases con atributos privados y métodos públicos.

### 🧠 Conceptos clave:

* Una función `void method() const;` garantiza que **no modificará el estado del objeto**.
* Un atributo `const` debe ser inicializado **en la lista de inicialización del constructor**.

```cpp
class Example {
private:
    const int _id;

public:
    Example(int id) : _id(id) {}
    int getId() const { return _id; }
};
```

Este patrón es útil para clases con atributos inmutables o identificadores únicos.

---

## 📁 ex02 – Strings y Manipulación de Texto con Clases

### 🎯 Objetivo:

Reforzar la comprensión del **paso de objetos como referencia**, el uso de **streams** (`std::cout`, `std::cin`) y de **métodos encapsulados**.

### 🔧 Recursos útiles:

* `std::string`, `std::getline()`
* Métodos como `.empty()`, `.length()`, `.find()`, `.replace()`

```cpp
void shout(std::string &text) {
    for (size_t i = 0; i < text.length(); i++)
        text[i] = std::toupper(text[i]);
}
```

---

## 📁 ex03 – Copia, Constructores y Destructores

### 🎯 Objetivo:

Practicar la **regla de los tres**: constructor por defecto, constructor por copia, destructor.

### 🧠 Conceptos clave:

* **Constructor por copia**: se usa cuando pasamos objetos por valor o devolvemos por valor.
* **Destructor**: se usa para liberar recursos (aunque aquí no usamos `new` todavía, es importante definirlo).

```cpp
class Sample {
public:
    Sample();
    Sample(const Sample &src);
    ~Sample();
};
```

> 💡 Importante: Aunque no se usa `new`/`delete`, se debe **declarar y entender** el comportamiento de estas funciones.

---

## 📁 ex04 – Sobrecarga de Operadores

### 🎯 Objetivo:

Entender cómo **sobrecargar el operador de asignación** (`operator=`) para clases personalizadas.

### 🧠 Teoría útil:

* En C++, puedes redefinir cómo actúan ciertos operadores con tus clases.
* Es importante cuando una clase **gestiona recursos propios** (como memoria dinámica).

```cpp
class MyObject {
private:
    int value;

public:
    MyObject &operator=(const MyObject &other) {
        this->value = other.value;
        return *this;
    }
};
```

> ☑️ Siempre devuelve `*this` por referencia para permitir cadenas de asignación: `a = b = c;`

---

## 📊 Consejos Generales

* Usa `-std=c++98` siempre para respetar las restricciones del proyecto.
* No implementes funciones en headers (`.hpp`), solo prototipos.
* Usa `const` correctamente para seguridad y claridad.
* Practica usando `std::cout`, `std::string` y construcciones típicas.

---

## 📚 Recursos Sugeridos

* [cplusplus.com - Classes](https://cplusplus.com/doc/tutorial/classes/)
* [cppreference.com](https://en.cppreference.com/)
* `man std::string`, `man const`, `man operator overloading`

---
