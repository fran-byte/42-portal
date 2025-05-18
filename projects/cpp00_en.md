---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 CPP00 – Introduction to C++ and Object-Oriented Programming

### 📌 Objective:

Introduce the basic concepts of C++: **classes**, **member functions**, **streams**, **const**, **static**, and initialization lists. Emphasis on object-oriented styles following the C++98 standard.

---

## 🔹 What is a class?

A **class** in C++ is a **template** for creating objects. It defines:

* **Attributes** (also called fields or members): represent the state of the object.
* **Methods** (also called member functions): represent the behavior of the object.

---

## 🔸 Attributes (Member Variables)

**Attributes** are variables declared inside the class. They can have different access levels:

```cpp
class Animal {
private:
    std::string _species;
    int _age;
};
```

* By convention, attributes are defined as `private` to protect them from being accessed directly from outside.
* Each **instance (object)** of the class has its **own copy** of these attributes.

---

## 🔸 Methods (Member Functions)

Methods allow the object to **do something** or for other code to **interact with it**.

```cpp
class Animal {
public:
    void makeSound();
    void sleep();
};
```

These methods would be called from outside like this:

```cpp
Animal dog;
dog.makeSound();
```

---

## 🔸 Constructors

A **constructor** is a special function that runs automatically when an object is created.

```cpp
class Animal {
public:
    Animal(); // Default constructor
};
```

It can also be overloaded:

```cpp
class Animal {
public:
    Animal(std::string type, int years);
};
```

The goal of a constructor is to **initialize** the object with valid values from the beginning.

---

## 🔸 Destructors

A **destructor** runs automatically when an object **goes out of scope** or is **deleted**. Its purpose is to **free resources**, although for simple objects, it may be empty.

```cpp
class Animal {
public:
    ~Animal(); // Destructor
};
```

---

## 🔸 Setters and Getters

To safely access `private` attributes, we use **public methods** called **setters** and **getters**.

### ✅ Setter

A method that **assigns a value** to an attribute:

```cpp
void setSpecies(std::string newSpecies) {
    _species = newSpecies;
}
```

### ✅ Getter

A method that **returns the value** of an attribute:

```cpp
std::string getSpecies() const {
    return _species;
}
```

> The `const` modifier means the method **does not change** the object’s state.

---

## 🧩 Full Example:

```cpp
class Animal {
private:
    std::string _species;
    int _age;

public:
    // Constructor
    Animal(std::string sp, int ag) : _species(sp), _age(ag) {}

    // Destructor
    ~Animal() {}

    // Setter
    void setAge(int ag) {
        _age = ag;
    }

    // Getter
    int getAge() const {
        return _age;
    }

    void speak() const {
        std::cout << "I am a " << species << " and I am " << age << " years old." << std::endl;
    }
};
```

And its usage:

```cpp
Animal cat("Feline", 3);
cat.speak();
cat.setAge(4);
std::cout << "Updated age: " << cat.getAge() << std::endl;
```

---

## 📌 Summary

| Concept     | Purpose                                       |
| ----------- | --------------------------------------------- |
| Class       | Defines a new custom data type                |
| Attribute   | Internal state of an object                   |
| Method      | Functions that describe the object’s behavior |
| Constructor | Initializes the object upon creation          |
| Destructor  | Frees resources when the object is destroyed  |
| Setter      | Method to modify a private attribute          |
| Getter      | Method to read a private attribute            |

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
