---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 CPP00 – Introduction to C++ and Object-Oriented Programming

### 📌 Objective:

Introduce the basic concepts of C++: **classes**, **member functions**, **streams**, **const**, **static**, and initialization lists. Emphasis on object-oriented styles following the C++98 standard.


---

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

### 🎯 Goal:

* Write a program that converts input to **uppercase**.

### 📦 Details:

* Files: `megaphone.cpp`, `Makefile`
* Input: command-line arguments
* Output:

  * If no arguments: `* LOUD AND UNBEARABLE FEEDBACK NOISE *`
  * If there are arguments: print them in uppercase

```bash
$> ./megaphone Hello there
HELLO THERE
```

### 🧠 Useful Concepts:

* Using `std::string`, `std::toupper` (cctype)
* Iterating through strings with `for` loops
* Using `argc` and `argv[]`

---

## 📁 ex01 – My Awesome PhoneBook

### 🎯 Goal:

Create an interactive **contact book** with a maximum of 8 contacts, allowing the user to:

* Add (`ADD`)
* Search (`SEARCH`)
* Exit (`EXIT`)

### 📦 Details:

* Files: `*.cpp`, `*.hpp`, `Makefile`
* Two classes:

  * `PhoneBook`: manages contacts (static array of 8)
  * `Contact`: stores info for each contact

### 🧠 Considerations:

* If a 9th contact is added, it replaces the oldest one
* Fields: first name, last name, nickname, phone number, darkest secret
* Output table should truncate strings >10 characters with a trailing `.`

```bash
$> ./phonebook
ADD
SEARCH
EXIT
```

### 🔧 Useful Resources for Implementation:

* `std::string`, `std::getline()`
* `std::setw`, `std::right`, `std::left`, `std::cout`
* `stringstream` for formatting and truncating strings
* Basic input validation and `while` loops to keep the program running

### 🧩 Design Suggestion:

* `Contact` class: simple setters and getters for each field
* `PhoneBook` class: array of 8 contacts + cyclic index for replacement
* `displayTable()` method for SEARCH format and `displayDetails()` to show full contact info

---

## 📊 General Tips

* Always compile with:

```bash
c++ -Wall -Wextra -Werror -std=c++98
```

* Use meaningful names and UpperCamelCase format for classes
* Do not implement functions in headers (except for templates)
* Avoid memory leaks: use `delete` correctly (although this module doesn’t use `new`/`delete`)

---

## 📚 Resources

* [cplusplus.com](https://cplusplus.com/)
* [cppreference.com](https://en.cppreference.com/)
* `man string`, `man iomanip`, `man ctime`

---
